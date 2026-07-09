n8n workflows and examples

This folder contains notes and example code for n8n workflows mentioned in the 3-day plan.

1) Workflow: AIQAR_WhatsApp_Audit_Responder
- Trigger: Webhook (HTTP Request)
- Nodes: Webhook -> Set (response_message) -> Gmail (notify Ali)
- Make webhook public from n8n.cloud and paste the URL into your WhatsApp webhook or integration.

2) Workflow: AIQAR_AI_Audit_Generator
- Trigger: Webhook
- Nodes: Webhook -> Set (map incoming fields) -> Code (generate prompt) -> Gmail (+ Google Sheets optional)

Example Code node (JavaScript) to generate an audit prompt (replace with real API call to Claude/OpenAI if available):

const prompt = `Create a professional real estate property audit.\n\nProperty Details:\n- Type: ${$json.property_type}\n- Location: ${$json.location}\n- Current Price: Rs. ${$json.price}\n\nGenerate:\n1. Current listing analysis\n2. 3 improvements (specific)\n3. Estimated price increase %\n4. Next steps\n\nFormat as professional report.`;

return [{ json: { audit_report: prompt, contact: $json.contact, generated_at: new Date() } }];

Notes and checklists:
- Save your n8n Webhook URLs in this file or in a secure password manager.
- For Gmail node, connect with OAuth; for Google Sheets, create a sheet and share it with the service account used by n8n (if any).
- When testing, use Postman or curl to send sample JSON to the webhook URL to confirm the flow.
