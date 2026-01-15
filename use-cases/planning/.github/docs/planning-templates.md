# Planning Templates

## User Story Template
```markdown
**As a** [user type],
**I want to** [action/goal],
**so that** [benefit/value].

### Acceptance Criteria
- [ ] Given [context], when [action], then [expected result]
- [ ] [Additional criterion]
- [ ] [Additional criterion]

### Technical Requirements
- API endpoint: `GET /api/resource`
- Database schema changes: N/A
- Performance requirements: < 500ms response time

### Definition of Done
- Code reviewed and approved
- Unit tests written (>90% coverage)
- Integration tests passing
- Documentation updated
- Deployed to staging environment
```

## Sprint Planning Template
```markdown
## Sprint X (Dates)

### Sprint Goal
[Clear, measurable objective for the sprint]

### Capacity
- Total story points: [number]
- Available developers: [number]
- Holidays/time off: [hours]

### Backlog Items
| Story | Points | Priority | Owner | Status |
|-------|--------|----------|-------|--------|
| [Story 1] | [points] | [high/med/low] | [name] | [todo/InProgress/Blocked] |
| [Story 2] | [points] | [high/med/low] | [name] | [todo/InProgress/Blocked] |

### Risks and Dependencies
- [Risk 1]: [Mitigation strategy]
- [Dependency 1]: [Resolution plan]

### Definition of Done Checklist
- [ ] All stories meet acceptance criteria
- [ ] Code review completed
- [ ] Tests passing
- [ ] Documentation updated
- [ ] Stakeholder demo conducted
```

## Technical Risk Assessment Template
```markdown
## Risk Assessment Matrix

| Risk | Probability | Impact | Mitigation | Owner |
|------|-------------|--------|------------|-------|
| [Technical risk 1] | [High/Med/Low] | [High/Med/Low] | [Strategy] | [Team member] |
| [Technical risk 2] | [High/Med/Low] | [High/Med/Low] | [Strategy] | [Team member] |

## Common Technical Risks
1. **Database Performance**
   - Risk: Slow queries affecting user experience
   - Mitigation: Query optimization, indexing strategy

2. **Third-party Dependencies**
   - Risk: API changes or service downtime
   - Mitigation: Circuit breakers, fallback mechanisms

3. **Security Vulnerabilities**
   - Risk: Data breaches, unauthorized access
   - Mitigation: Regular security audits, dependency scanning

4. **Scalability Issues**
   - Risk: System cannot handle increased load
   - Mitigation: Load testing, horizontal scaling strategy
```