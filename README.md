{
  "name": "Data Processing Automation Workflow",
  "nodes": [
    {
      "parameters": {
        "operation": "xlsx",
        "options": {}
      },
      "type": "n8n-nodes-base.extractFromFile",
      "typeVersion": 1.1,
      "position": [
        896,
        208
      ],
      "id": "8a29dbc5-b443-4728-a18b-cb5229185e50",
      "name": "Extract from File"
    },
    {
      "parameters": {
        "jsCode": "// Calculate summary metrics from input items\nconst items = $input.all();\n\n// Initialize counters\nlet totalRecords = items.length;\nlet totalSales = 0;\n\n// Calculate total sales\nfor (const item of items) {\n  const salesAmount = item.json.sales || item.json.amount || 0;\n  totalSales += parseFloat(salesAmount) || 0;\n}\n\n// Calculate average sales\nconst averageSales = totalRecords > 0 ? totalSales / totalRecords : 0;\n\n// Return single item with calculated metrics\nreturn [\n  {\n    json: {\n      totalRecords: totalRecords,\n      totalSales: totalSales,\n      averageSales: averageSales\n    }\n  }\n];"
      },
      "id": "05ca9664-4d67-4cfa-a82c-55797a72fa23",
      "name": "Calculate Summary Metrics",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1120,
        208
      ]
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "id-1",
              "name": "summary",
              "value": "Summary Metrics",
              "type": "string"
            },
            {
              "id": "id-2",
              "name": "total_records",
              "value": "={{ $json.totalRecords }}",
              "type": "number"
            },
            {
              "id": "id-3",
              "name": "total_sales",
              "value": "={{ $json.totalSales }}",
              "type": "number"
            },
            {
              "id": "id-4",
              "name": "average_sales",
              "value": "={{ $json.averageSales }}",
              "type": "number"
            }
          ]
        },
        "options": {}
      },
      "id": "b9d3363b-d0e6-45b7-9290-c6edf0743f83",
      "name": "Format Output",
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        1344,
        208
      ]
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "upload_spreadsheet",
        "responseMode": "lastNode",
        "responseData": "firstEntryBinary",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2.1,
      "position": [
        448,
        208
      ],
      "id": "55faded5-dc79-496d-8128-7ca3d5cf608a",
      "name": "Webhook",
      "webhookId": "de8f91d0-216f-4ae5-96a1-16051c855d66"
    }
  ],
  "pinData": {},
  "connections": {
    "Extract from File": {
      "main": [
        [
          {
            "node": "Calculate Summary Metrics",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Calculate Summary Metrics": {
      "main": [
        [
          {
            "node": "Format Output",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Webhook": {
      "main": [
        [
          {
            "node": "Extract from File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "availableInMCP": false
  },
  "versionId": "10d178d8-6371-4e24-a1a2-967728167a33",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "fa13aa0d7a9e0d52fe0be26fe9cfd8911ea3503baf5f1ef78f3f3f026051d33a"
  },
  "id": "gVVKqb_VbR1at4QpzqC5F",
  "tags": []
}