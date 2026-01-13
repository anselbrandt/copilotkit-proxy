# CopilotKit Proxy Server

### [Self Hosting Copilot Runtime](https://docs.copilotkit.ai/direct-to-llm/guides/self-hosting)

### Express.js

```javascript
import express from "express";
import {
  CopilotRuntime,
  OpenAIAdapter,
  copilotRuntimeNodeHttpEndpoint,
} from "@copilotkit/runtime";

const app = express();

const serviceAdapter = new OpenAIAdapter();

app.use("/copilotkit", (req, res, next) => {
  (async () => {
    const runtime = new CopilotRuntime();
    const handler = copilotRuntimeNodeHttpEndpoint({
      endpoint: "/copilotkit",
      runtime,
      serviceAdapter,
    });

    return handler(req, res);
  })().catch(next);
});

app.listen(4000, () => {
  console.log("Listening at http://localhost:4000/copilotkit");
});
```

### Node.js HTTP

```javascript
import { createServer } from "node:http";
import {
  CopilotRuntime,
  OpenAIAdapter,
  copilotRuntimeNodeHttpEndpoint,
} from "@copilotkit/runtime";

const serviceAdapter = new OpenAIAdapter();

const server = createServer((req, res) => {
  const runtime = new CopilotRuntime();
  const handler = copilotRuntimeNodeHttpEndpoint({
    endpoint: "/copilotkit",
    runtime,
    serviceAdapter,
  });

  return handler(req, res);
});

server.listen(4000, () => {
  console.log("Listening at http://localhost:4000/copilotkit");
});
```
