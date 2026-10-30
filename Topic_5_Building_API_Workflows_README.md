# Topic 5 - Building API Workflows

**Course:** n8n Hands-On API Integration  
**Deliverable:** Workflow README and assessment evidence  
**Evidence source:** Five n8n screenshots documented in `Topic_5_Building_API_Workflows_Evidence.pdf`

## Objective
Demonstrate an end-to-end n8n API workflow that prepares test user data, calls an HTTP GET echo API with a custom header, sends a JSON POST request to a mock endpoint, and formats execution metadata.

## Workflow architecture

```text
Manual Trigger
    |
Set Base User
    |
Postman Echo Headers (GET)
    |
Create Log Entry (POST)
    |
Output Metadata
```

## Node-by-node implementation

| Node | Purpose | Observed result |
| --- | --- | --- |
| Manual Trigger | Starts the workflow on demand | Successful execution |
| Set Base User | Maps `username` and `department` | `Alice`, `Engineering` |
| Postman Echo Headers | GET `https://postman-echo.com/headers` with custom `x-user-dept` header | Echoed `x-user-dept: Engineering` and `user-agent: n8n` |
| Create Log Entry | POST JSON to `https://jsonplaceholder.typicode.com/posts` | Response includes title `Log entry for Alice` and mock ID `101` |
| Output Metadata | Maps execution and workflow identifiers and final title | Execution ID `548598`, workflow ID `jgJnQLyPUW7UzLb`, title `Log entry for Alice` |

## Test procedure

1. Open the Topic 5 workflow in n8n.
2. Run the Manual Trigger / **Execute workflow**.
3. Check that `Set Base User` produces one item containing `username` and `department`.
4. Open `Postman Echo Headers` and inspect the returned `headers` object for `x-user-dept: Engineering`.
5. Open `Create Log Entry` and verify the response title and example ID.
6. Open `Output Metadata` and verify `executionId`, `workflowId`, and `finalLogTitle`.
7. Capture the successful execution view and each relevant node's output.

## Evidence summary

| Test | Expected outcome | Evidence status |
| --- | --- | --- |
| Workflow runs end to end | Five nodes complete | PASS - screenshot |
| User mapping | Alice / Engineering | PASS - screenshot |
| Header forwarding | `x-user-dept: Engineering` | PASS - screenshot |
| JSON POST | Response includes `Log entry for Alice` | PASS - screenshot |
| Metadata output | Execution and workflow IDs with final title | PASS - screenshot |
| Persistent database logging | Durable record exists | NOT TESTED - mock endpoint only |

## Important limitations

- JSONPlaceholder is a **mock API**. A POST response with `id: 101` is not proof of persistent storage.
- The available screenshots do not show every hidden node setting or expression. This README describes only the observable configuration and results.
- Do not place API keys or credentials in exported workflow files or screenshots.
- The workflow export JSON and video recording are **not included** in this README or evidence PDF; attach them separately if required by the LMS.

## Submission package

- `Topic_5_Building_API_Workflows_README.md` - this implementation and verification summary.
- `Topic_5_Building_API_Workflows_Evidence.pdf` - screenshots and observed execution evidence.
- **To attach separately:** exported n8n workflow `.json` and demonstration video/link, if required by the assessment.

## Suggested demo outline (3-5 minutes)

1. Introduce the objective and workflow layout.
2. Explain the base user fields and how the GET request echoes the department header.
3. Show the POST body and mock API response.
4. Explain the final metadata mapping.
5. Run the workflow, show green checks and output, and mention the mock API persistence limitation.
