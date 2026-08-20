# Transformation examples

Use these examples as patterns, not templates to copy mechanically.

## Dense explanation to layered explanation

### Before

> The service, which is responsible for receiving events that may originate from
> several external systems and which are not necessarily delivered in the order
> in which they were generated, will attempt, where possible, to process those
> events in a manner that avoids duplication, although consumers should not rely
> on this behavior when a reliable exactly-once guarantee is required.

### After

> The service receives events from several external systems. Events may arrive
> out of order.
>
> The service usually avoids processing the same event twice. It does not
> provide an exactly-once guarantee. Consumers that require exactly-once
> processing must add their own deduplication.

The rewrite keeps the delivery behavior, limitation, and required consumer
action. It makes the actor, conditions, and consequence visible.

## Buried outcome to front-loaded procedure

### Before

> After checking the configuration and making sure that the worker has access to
> the queue, you can use the command below, although it is important to note
> that the command will fail if the local environment has not been initialized,
> which is something that can be done by following the setup instructions.

### After

> Start the worker after you initialize the local environment and grant it queue
> access.
>
> 1. Initialize the environment by following [the setup guide].
> 2. Confirm that the worker can access the queue.
> 3. Run the command below:
>
>    ```shell
>    worker start
>    ```
>
> If the environment is not initialized, the command fails.

The rewrite turns prerequisites into explicit steps and keeps the failure state
visible without adding new requirements.

## Generic heading to findable heading

| Weak heading | Stronger heading |
| --- | --- |
| Overview | What this service does |
| Configuration | Configure retry limits |
| Considerations | Limits and failure modes |
| More information | Authentication reference |

The stronger headings improve information scent. They are not required to use a
verb when the section is a reference entry rather than an action.

## Section anatomy and block roles

### Before

````markdown
## Configuration

The service has a retry limit and a log level and you can configure these in the
environment file, but if you use a value above the allowed maximum the service
will reject it and when debugging you may also want to change the log level.

### Resetting

The reset command is useful locally.

### More details

You can read more in the reference.
````

The content is present, but the section does not distinguish configuration,
validation, destructive behavior, or the next path. The headings are generic and
the reader must infer which information is required.

### After

````markdown
## Configure retry behavior

Set the retry limit and log level in `.env` before starting the service.

- **Default retry limit:** `5`
- **Maximum retry limit:** `20`
- **Optional:** Set `LOG_LEVEL` to increase local diagnostic output.

The service rejects retry limits above `20`.

### Reset local data

Use the reset command only when you want to delete local Redis data:

```shell
npm run reset
```

> [!WARNING]
> This command deletes all local Redis data and cannot be undone.

For the complete list of environment variables, read the [configuration
reference](configuration.md).
````

This version gives the section one purpose, introduces the point, uses inline
code for literal values, uses a fenced block for a copyable command, separates a
destructive action, and gives the warning a clear reason to stand out. The
warning is not the only place where the irreversible effect is stated.

## Distinguish block roles

Use a block because its content has a different job:

| Block | Job | Example content |
| --- | --- | --- |
| Orientation | Establish relevance and route | Outcome, audience, prerequisites, next action |
| Action | Tell the reader what to do | Numbered steps or a command with context |
| Evidence | Support a claim or decision | Data, rationale, result, or citation |
| Example | Make an abstract idea concrete | Input and output, scenario, or worked case |
| Boundary | Prevent a wrong action | Warning, exception, constraint, or uncertainty |
| Reference | Support lookup and depth | Parameters, definitions, links, or edge cases |
| Exit | Help the reader continue | Expected result, next step, or related guide |

Keep related blocks together. Do not make visual treatment carry information
that is absent from the text, and do not create separate blocks for every small
variation in emphasis.

## Complex content without false simplicity

When a concept has unavoidable complexity, use this order:

1. State the short operational meaning.
2. Name the exact term and define it.
3. Show the smallest correct example.
4. Explain the important exception or tradeoff.
5. Link to the complete reference.

Do not replace a formal definition with an analogy unless the analogy is labeled
and the formal meaning remains available.

## Callout audit

Before adding a callout, ask:

- Does the reader need this information to avoid harm, error, or a wrong choice?
- Is it easier to notice because it is separated from the main flow?
- Would a descriptive heading or sentence be clearer and less visually heavy?

If the answer is no, keep the content in the normal flow.
