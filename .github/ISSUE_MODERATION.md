# Issue Moderation Configuration

This repository includes an automated GitHub Action that moderates issues and comments based on team membership.

## How it works

The GitHub Action (`issue-moderation.yml`) automatically:

1. **Monitors new issues**: When someone creates an issue, it checks if they're a member of authorized teams
2. **Monitors new comments**: When someone comments on an issue, it checks their team membership
3. **Takes action**: If the user is not in an authorized team:
   - Issues: Closes the issue and adds an explanatory comment
   - Comments: Deletes the comment immediately

## Configuration

To configure which teams are authorized, edit the `allowedTeams` array in `.github/workflows/issue-moderation.yml`:

```javascript
const allowedTeams = [
  'core-team',        // Replace with your actual team slugs
  'maintainers',      // Team slugs are found in your GitHub organization
  'admins'            // Multiple teams can be authorized
];
```

## Team Setup

1. Ensure your GitHub organization has teams created
2. Add the appropriate members to each team
3. Update the `allowedTeams` array with your team slugs
4. The workflow will automatically enforce these permissions

## Permissions Required

The workflow requires the following permissions:
- `issues: write` - To close issues and create/delete comments
- `contents: read` - To access repository content
- `metadata: read` - To read organization metadata and team information

## Important Notes

- Only organization teams are supported (not repository collaborators)
- Team membership is checked against the organization that owns the repository
- The action provides clear logging for all moderation activities
- Users will receive a clear message when their issue is closed due to team membership