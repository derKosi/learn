In this exercise, you'll build and deploy an AI agent using Microsoft Foundry Agent Service. You'll create an agent, configure its instructions and tools, test it in the playground, and deploy it for integration with applications.

## Exercise objectives

By completing this exercise, you'll:

- Create a Microsoft Foundry project with necessary resources
- Build an AI agent with custom instructions
- Add tools to extend agent capabilities
- Test the agent using the integrated playground
- Deploy the agent to Microsoft Foundry
- Generate integration code for the agent

## Before you start

To complete this exercise, you need:

- An active Azure subscription with permission to create resources
- Visual Studio Code installed on your machine (or use the Azure portal)
- The Microsoft Foundry extension for VS Code (if using VS Code approach)

## Exercise steps

### Task 1: Set up your Microsoft Foundry environment

1. Sign in to the Azure portal at https://portal.azure.com
1. Navigate to Microsoft Foundry at https://ai.azure.com
1. Create a new project or select an existing one
1. Ensure you have a deployed model (such as GPT-4o)

### Task 2: Create an AI agent

**Using the Azure portal:**

1. In Microsoft Foundry, navigate to your project
1. Select **Agents** from the left menu
1. Select **Create** to create a new agent
1. Enter a name for your agent (for example, "Customer Service Assistant")
1. Select your deployed model
1. Add a description

**Using Visual Studio Code:**

1. Open VS Code and ensure the Microsoft Foundry extension is installed
1. Sign in to Azure and select your project
1. In the Azure Resources view, find the Agents section
1. Select the **+** icon to create a new agent
1. Configure the agent name and model in the Designer

### Task 3: Configure agent instructions

Write instructions for your agent that define its role and behavior. For a customer service assistant:

```text
You're a helpful customer service agent for Contoso Retail. You assist customers with:
- Product information and recommendations
- Order status inquiries
- Returns and refunds
- Store locations and hours

Guidelines:
- Be friendly and professional
- Ask clarifying questions when requests are ambiguous
- For order-specific questions, use tools to look up information
- If you can't help with something, explain what you can do instead

Keep responses concise but helpful.
```

### Task 4: Add tools to your agent

Add the following tools to extend your agent's capabilities:

1. **Code Interpreter** - For calculations and data processing
1. **Bing Search** - For current product information and general knowledge
1. **File Search** (optional) - If you have product documentation to upload

For File Search:
- Create a new vector store
- Upload sample product documentation
- Configure the agent to use the vector store

### Task 5: Test your agent

1. Open the playground (in Azure portal or VS Code)
1. Test these scenarios:
   - "What products do you offer?"
   - "Can you help me find information about [current topic]?"
   - "Calculate the total cost of 3 items at $29.99 each with 8% tax"
1. Verify the agent responds appropriately
1. Check that tools are invoked when expected

### Task 6: Deploy your agent

**In Azure portal:**
1. Review your agent configuration
1. Select **Deploy**
1. Wait for deployment to complete

**In VS Code:**
1. In the Agent Designer, select **Create on Microsoft Foundry**
1. Wait for deployment confirmation
1. Refresh the Azure Resources view

### Task 7: Generate integration code

1. Select your deployed agent
1. Generate sample code (VS Code: **Open Code File**)
1. Review the generated code
1. Note the agent ID and project details for integration

## Verification

After completing the exercise, verify:

- Your agent appears in the deployed agents list
- You can interact with it in the playground
- Tools work as expected during conversations
- You have sample integration code

## Clean up

If you don't plan to use these resources further:

1. Navigate to your Azure resource group
1. Delete the resource group to remove all resources
1. Confirm deletion

Congratulations! You've successfully built and deployed an AI agent using Microsoft Foundry Agent Service.
