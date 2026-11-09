# 🌐 Commonwealth Medical Marijuana Platform — Data 360 Lakehouse Project

**Target Salesforce Org:** `data-cloud-dev-org-1`  
**Org ID:** `00Daj00001ENcoqEAD`  
**Admin User:** `dipankar.sahoo.7999845712a7@agentforce.com`  
**Architecture Role:** Ingestion Lakehouse, High-Volume Sensor / Telemetry Storage & Analytical Store  

---

## 1. Project Overview & Directory Layout

This project encapsulates all metadata, data stream configurations, External Client Apps (ECAs), and ingestion REST endpoints for the **Commonwealth Medical Marijuana Regulatory Lakehouse**:

```
marijuana Data Cloud/
├── sfdx-project.json               # Independent Salesforce DX configuration
├── manifest/
│   └── package.xml                 # Master deployment manifest for Data Cloud
├── force-app/main/default/
│   ├── externalClientApps/         # Modern External Client App (Data360_Lakehouse_ECA)
│   ├── extlClntAppGlobalOauthSets/ # ECA Global OAuth Settings (Callback URL)
│   ├── extlClntAppOauthSettings/   # ECA OAuth Settings (Scopes: Api, RefreshToken)
│   ├── dataSourceObjects/          # Lakehouse Data Source Objects
│   └── permissionsets/             # MMAP_Lakehouse_Ingest_PermSet
└── docs/                           # Segregated Data Cloud documentation:
    ├── DATA_CLOUD_LAKEHOUSE_SPECIFICATION.md
    └── DATA_360_INTEGRATION_AND_CONNECTION_PLAN.md
```

---

## 2. CLI Deployment Commands

Deploy metadata directly to the Data 360 org:
```bash
sf project deploy start -d force-app/main/default -o data-cloud-dev-org-1
```

Or deploy using the manifest:
```bash
sf project deploy start --manifest manifest/package.xml -o data-cloud-dev-org-1
```

Validate deployment against Data 360 org:
```bash
sf project deploy validate --manifest manifest/package.xml -o data-cloud-dev-org-1
```

---

## 3. Querying Lakehouse Telemetry Data (DMO)

Query the native Data Cloud Lakehouse Data Model Object (`MMAP_Telemetry__dlm`) via Data Cloud Query API v2:
```bash
sf apex run -o pmarijuna-partner-dev-org -e "Map<String, Object> res = Data360Service.queryTelemetryEvents('PKG-2026-TEST-001', 10, 0); System.debug(JSON.serializePretty(res));"
```
