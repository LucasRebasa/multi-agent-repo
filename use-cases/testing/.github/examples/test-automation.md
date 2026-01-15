# Test Automation Examples

## Unit Testing (Jest)
```javascript
// userService.test.js
const userService = require('../services/userService');
const User = require('../models/User');

// Mock dependencies
jest.mock('../models/User');

describe('UserService', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });

  describe('createUser', () => {
    it('should create a user with valid data', async () => {
      // Arrange
      const userData = { name: 'John Doe', email: 'john@example.com' };
      const expectedUser = { id: 1, ...userData };
      User.create.mockResolvedValue(expectedUser);

      // Act
      const result = await userService.createUser(userData);

      // Assert
      expect(User.create).toHaveBeenCalledWith(userData);
      expect(result).toEqual(expectedUser);
    });

    it('should throw error for invalid email', async () => {
      // Arrange
      const userData = { name: 'John Doe', email: 'invalid-email' };

      // Act & Assert
      await expect(userService.createUser(userData))
        .rejects
        .toThrow('Invalid email format');
    });
  });
});
```

## Integration Testing (Spring Boot Test)
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@Transactional
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
public class UserControllerIntegrationTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Autowired
    private UserRepository userRepository;

    @Test
    public void whenCreateUser_thenReturns201() {
        // Given
        UserDto userDto = new UserDto("John Doe", "john@example.com");
        
        // When
        ResponseEntity<User> response = restTemplate.postForEntity(
            "/api/users", userDto, User.class);
        
        // Then
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertNotNull(response.getBody().getId());
        assertEquals("John Doe", response.getBody().getName());
        
        // Verify database state
        assertTrue(userRepository.existsById(response.getBody().getId()));
    }
}
```

## End-to-End Testing (Playwright)
```javascript
// e2e.spec.js
const { test, expect } = require('@playwright/test');

test.describe('User Registration Flow', () => {
  test('should register new user successfully', async ({ page }) => {
    // Navigate to registration page
    await page.goto('/register');
    
    // Fill registration form
    await page.fill('[data-testid=name-input]', 'John Doe');
    await page.fill('[data-testid=email-input]', 'john@example.com');
    await page.fill('[data-testid=password-input]', 'SecurePassword123!');
    await page.fill('[data-testid=confirm-password-input]', 'SecurePassword123!');
    
    // Submit form
    await page.click('[data-testid=register-button]');
    
    // Verify success message
    await expect(page.locator('[data-testid=success-message]'))
      .toHaveText('Registration successful!');
    
    // Verify redirect to dashboard
    await expect(page).toHaveURL('/dashboard');
  });
  
  test('should show validation error for duplicate email', async ({ page }) => {
    // Pre-existing user in database
    await page.goto('/register');
    
    // Fill with existing email
    await page.fill('[data-testid=name-input]', 'Jane Doe');
    await page.fill('[data-testid=email-input]', 'existing@example.com');
    await page.fill('[data-testid=password-input]', 'SecurePassword123!');
    await page.fill('[data-testid=confirm-password-input]', 'SecurePassword123!');
    
    // Submit form
    await page.click('[data-testid=register-button]');
    
    // Verify error message
    await expect(page.locator('[data-testid=error-message]'))
      .toHaveText('Email already exists');
  });
});
```

## API Testing (Postman/Newman)
```javascript
// postman-collection.json
{
  "info": {
    "name": "User API Tests",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Create User",
      "request": {
        "method": "POST",
        "header": [
          {
            "key": "Content-Type",
            "value": "application/json"
          }
        ],
        "body": {
          "mode": "raw",
          "raw": '{\n  "name": "Test User",\n  "email": "test@example.com"\n}'
        },
        "url": {
          "raw": "{{base_url}}/api/users",
          "host": ["{{base_url}}"],
          "path": ["api", "users"]
        }
      },
      "event": [
        {
          "listen": "test",
          "script": {
            "exec": [
              "pm.test('Status code is 201', function () {",
              "    pm.response.to.have.status(201);",
              "});",
              "",
              "pm.test('Response has required fields', function () {",
              "    var jsonData = pm.response.json();",
              "    pm.expect(jsonData).to.have.property('id');",
              "    pm.expect(jsonData).to.have.property('name');",
              "    pm.expect(jsonData).to.have.property('email');",
              "});",
              "",
              "pm.test('Response time is less than 500ms', function () {",
              "    pm.expect(pm.response.responseTime).to.be.below(500);",
              "});"
            ]
          }
        }
      ]
    }
  ]
}
```