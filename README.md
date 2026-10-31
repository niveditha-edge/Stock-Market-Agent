# Stock Market AI Agent using Microsoft Foundry and Azure

An AI-powered Stock Market Agent built using **Microsoft Foundry, Azure Logic Apps, Model Context Protocol (MCP), Alpha Vantage API, and Azure Table Storage**.

This project demonstrates how AI agents can retrieve stock market data, interact with external tools, store information in the cloud, and perform calculations using Python.

## Project Status

<badge color="success">Completed and Tested</badge>

- **Development:** Completed
- **Testing:** Successfully tested with valid and invalid stock symbols.
- **Azure Deployment:** Built and tested using Microsoft Azure.
- **Current Availability:** Not currently deployed or running.
- **Resource Cleanup:** Azure resources were deleted after testing to avoid ongoing cloud charges.

**Note:** This repository documents a completed hands-on project. The live Azure agent and its associated cloud services are no longer active.

## Project Overview

The Stock Market AI Agent uses Microsoft Foundry Agent Service to coordinate multiple tools and perform stock market-related tasks.

The agent can:
- Retrieve stock quotes using the Alpha Vantage API.
- Connect to external tools using OpenAPI and MCP.
- Save stock quote information in Azure Table Storage.
- Use Python through Foundry Code Interpreter to calculate stock price metrics.
- Generate a simple analysis based on retrieved stock information.

## Architecture

The project consists of three main layers:

1. **AI Layer:** Microsoft Foundry hosts the StockMarketAgent and coordinates tool calls.
2. **Integration Layer:** Azure Logic Apps exposes the stock-saving workflow through an MCP server.
3. **Storage Layer:** Azure Table Storage stores the retrieved stock quote information.

### Architecture Flow

```text
              User Prompt
                  |
                  v
       Microsoft Foundry Agent
          (StockMarketAgent)
                  |
       +----------+-----------+
       |          |           |
       v          v           v
   OpenAPI      MCP Tool   Code Interpreter
    Tool           |         (Python)
       |           |
       v           v
 Alpha Vantage  Azure Logic Apps
      API       SaveStockQuote
                    |
                    v
             Azure Table Storage
               (StockQuotes)
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Microsoft Foundry | Building and managing the AI agent |
| GPT-5.4-mini | Language model used by the agent |
| Azure Logic Apps | Creating the stock-saving workflow |
| MCP (Model Context Protocol) | Connecting the agent with external tools |
| Azure Table Storage | Storing stock quote information |
| Alpha Vantage API | Retrieving stock market data |
| Python | Stock price calculations and analysis |
| Foundry Code Interpreter | Running Python in a sandbox |
| OpenAPI | Connecting the stock market API |

## Tools and Integrations

### 1. Alpha Vantage API – Stock Data Retrieval

The agent uses the Alpha Vantage API to retrieve stock market information through its `GLOBAL_QUOTE` operation.

The retrieved information includes:
- Stock symbol
- Latest trading price
- Opening price
- Highest price
- Lowest price
- Trading volume
- Price change
- Percentage change

### 2. MCP Server – Stock Data Storage

The project uses an MCP server hosted through Azure Logic Apps.

The MCP tool, `stock-storage-mcp`, exposes the `SaveStockQuote` workflow.

Its responsibilities include:
- Receiving stock quote details from the agent.
- Passing the information to the Logic Apps workflow.
- Saving the stock data in Azure Table Storage.
- Returning a confirmation response to the agent.

### 3. Azure Table Storage

Azure Table Storage is used to store stock quote records.

The table name is:

`StockQuotes`

The records use:
- **PartitionKey:** Stock symbol.
- **RowKey:** Save timestamp.

This structure allows stock records to be grouped by their stock symbols.

### 4. Code Interpreter – Stock Analysis

Microsoft Foundry Code Interpreter executes Python code in a sandboxed environment.

It helps calculate:
- Daily price range.
- Price movement.
- Percentage change.
- Stock price position within the day's high and low range.

The agent uses these calculations to generate its analysis.

## Project Workflow

1. The user enters a stock-related prompt in the Microsoft Foundry playground.
2. The agent identifies the required tools.
3. The OpenAPI tool retrieves stock information from Alpha Vantage.
4. The agent sends the retrieved information to the MCP tool.
5. Azure Logic Apps executes the `SaveStockQuote` workflow.
6. The stock quote is stored in Azure Table Storage.
7. Code Interpreter performs Python-based calculations.
8. The agent presents the retrieved information and analysis to the user.

## Testing

The agent was tested using different prompts.

### Test 1: Valid Stock Symbol

```text
Get the latest quote for MSFT, save it, and analyze it.
```

Expected behavior:
- Retrieve the stock quote.
- Request approval for the MCP tool call when required.
- Save the stock quote in Azure Table Storage.
- Perform calculations using Code Interpreter.
- Return the stock analysis.

### Test 2: Invalid Stock Symbol

```text
Get the latest quote for ZZZZ, save it, and analyze it.
```

Expected behavior:
- Handle the invalid or unavailable stock data.
- Avoid saving invalid stock information.
- Return an appropriate response.

## Key Learnings

Through this project, I gained practical experience in:

- Building AI agents using Microsoft Foundry.
- Understanding agent tool calling and orchestration.
- Integrating external APIs using OpenAPI.
- Understanding and implementing MCP-based tool integration.
- Creating workflows using Azure Logic Apps.
- Storing structured information in Azure Table Storage.
- Using Python through Code Interpreter for calculations.
- Testing AI agent workflows and handling invalid inputs.
- Working with Microsoft Azure cloud services.

## Learning Experience – Global AI On Tour, Chennai

I attended **Global AI On Tour – Chennai**, organized by the Global AI Community at the Microsoft office in Chennai.

The event provided valuable insights into emerging AI technologies and practical applications of agentic AI.

### Sessions and Topics Explored

- **Building AI Agents with Microsoft Foundry and MCP with Azure Logic Apps**
- **Smart Manufacturing: Automating Factory Floor Visual Defect Detection with Multimodal AI using Microsoft Foundry and n8n**
- **Synergizing Agentic AI: Mastering OpenClaw Integration in Microsoft Foundry**

These sessions helped me understand:
- AI agents and agentic AI.
- Model Context Protocol (MCP).
- Multimodal AI applications.
- Workflow automation.
- Integrating AI agents with external tools and services.

Inspired by these sessions, I used the Azure credits provided during the event to build and test my own **Stock Market AI Agent** using Microsoft Foundry and Azure.

This project gave me an opportunity to apply the concepts I learned during the event through hands-on implementation.

## Security Notes

- API keys and credentials should be stored securely using connections or appropriate secret-management mechanisms.
- Do not commit API keys, connection strings, workflow signatures, or MCP credentials to GitHub.
- Use environment variables or secure Azure connections for sensitive information.

## Deployment and Resource Cleanup

This project was built and tested using Azure resources.

After completing the implementation and testing, the Azure resource group was deleted to avoid ongoing cloud charges.

Therefore, the Azure services used for this project are not currently running.

## Acknowledgements

Special thanks to:
- **Global AI Community** for organizing Global AI On Tour – Chennai.
- **Microsoft** for providing the opportunity to explore Azure and Microsoft Foundry.
- Everyone who contributed to making this learning experience valuable.

## Tags

`Microsoft Foundry` `Azure` `AI Agents` `Agentic AI` `MCP` `Python` `Azure Logic Apps` `Alpha Vantage` `Azure Table Storage` `OpenAPI` `Generative AI`

