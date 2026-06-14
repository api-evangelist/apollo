# Apollo.io GraphQL API

Apollo.io provides a GraphQL API alongside its REST API, accessible at `https://api.apollo.io/api/v1/`. The GraphQL interface exposes the full breadth of Apollo's B2B sales intelligence platform — contacts, organizations, sequences, tasks, opportunities, accounts, deals, users, teams, email templates, enrichment, and webhooks — in a single queryable schema.

## Endpoint

```
https://api.apollo.io/api/v1/graphql
```

## Authentication

All requests require an Apollo API key passed as a header:

```
X-Api-Key: <your_api_key>
```

OAuth 2.0 bearer tokens are also accepted for partner integrations:

```
Authorization: Bearer <access_token>
```

Obtain API keys from the Apollo UI under **Settings > Integrations > API Keys**.

## Capabilities

### Contacts and People

Query and mutate contact records from Apollo's database of 230M+ verified contacts. Retrieve full contact details including emails, phone numbers, job history, and social profiles. Use `searchContacts` to filter by title, location, seniority, industry, technology stack, and dozens of other criteria.

### Organizations

Access Apollo's database of 30M+ companies. Search by industry, headcount, revenue range, technology stack, funding stage, and geographic region. Retrieve detailed company profiles including funding history, technologies used, and current employee counts.

### Sequences

Manage outreach sequences programmatically. Create and update multi-step sequences that combine email, phone, LinkedIn, and task steps. Enroll contacts into sequences and monitor engagement metrics.

### Tasks

Create, assign, and complete tasks tied to contacts, accounts, and opportunities. Filter tasks by type (email, call, LinkedIn, general), status, assignee, and due date.

### Opportunities and Deals

Manage the full sales pipeline. Create opportunities, update deal stages, track deal values and close dates, and associate contacts and accounts with opportunities.

### Accounts

Manage account records that mirror your CRM. Score accounts based on fit and intent signals, and link contacts and deals to accounts.

### Data Enrichment

Enrich individual contacts and organizations with Apollo's verified data. Bulk enrich lists of up to 10,000 records per request. Verify email deliverability before sending outreach.

### Users and Teams

Manage team members, roles, and permissions. Query user activity and assign tasks and sequences to specific team members.

### Email Templates and Snippets

Create and manage reusable email templates and personalization snippets for use in sequences and one-off outreach.

### Webhooks

Register and manage webhook endpoints to receive real-time event notifications for contact updates, email events, task completions, and deal stage changes.

## Schema Reference

See `apollo-schema.graphql` for the full type definitions.

## Example Query

```graphql
query SearchContacts($filter: SearchFilter!) {
  searchContacts(filter: $filter) {
    pageInfo {
      totalCount
      page
      perPage
    }
    contacts {
      id
      firstName
      lastName
      title
      organization {
        id
        name
        websiteDomain
      }
      contactEmails {
        email
        emailStatus
      }
      contactPhones {
        number
        type
      }
    }
  }
}
```

## Example Mutation

```graphql
mutation EnrollContactInSequence($contactId: ID!, $sequenceId: ID!) {
  enrollContactInSequence(contactId: $contactId, sequenceId: $sequenceId) {
    sequenceContact {
      id
      status
      currentStep
    }
  }
}
```

## Rate Limits

GraphQL requests share the same rate limit pool as REST API calls. Limits vary by plan:

| Plan       | Requests / Minute |
|------------|------------------|
| Free       | 50               |
| Basic      | 200              |
| Professional | 500            |
| Organization | 1000           |

Exceeding the limit returns HTTP 429. Retry after the interval specified in the `Retry-After` response header.

## Resources

- [Apollo API Documentation](https://docs.apollo.io/reference)
- [Apollo API Getting Started](https://docs.apollo.io/docs)
- [Apollo API Tutorials](https://docs.apollo.io/docs/overview-apollo-api-tutorials)
- [Authentication Guide](https://docs.apollo.io/reference/authentication)
- [Rate Limits](https://docs.apollo.io/reference/rate-limits)
- [Apollo Developer Community](https://community.apollo.io/)
