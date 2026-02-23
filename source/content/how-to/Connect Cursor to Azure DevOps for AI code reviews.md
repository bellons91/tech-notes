A deeper integration with an Azure DevOps MCP server can significantly improve the shaping of agent context during its reasoning. By pulling work item metadata, the agent can drive its output to the actual intent behind each task, leading to more aligned code changes.

Online docs provide different MCP servers to connect to: [https://cursor.com/docs/context/mcp#servers](https://cursor.com/docs/context/mcp#servers "https://cursor.com/docs/context/mcp#servers").

Select the ADO one and click on "Add to Cursor": as a result, a new MCP server with a large set of tools will be added to "Tools & MCP section" of our Cursor's settings. We can edit the configuration of the installed MCP server to add a PAT for ADO access, this way:

![[Pasted image 20260223180026.png]]
A PAT can be created through the "Personal access tokens" section of our ADO profile. 

As a real use case, this MCP server enablement helped me aiding another developer in finding out what was the best solution to apply to a design flaw in a PR, by connecting to the ADO platform, searching for the specific pull request ID, going through the commits and understanding what was the flaw and which were the possible ways around it.