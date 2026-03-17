# Never Republish Again!
### Using the ArcGIS API for Python to Manage and Administer Hosted Feature Layers

Workshop materials for the **WLIA (Wisconsin Land Information Association) AGO HFL Management** session. This repository contains a series of Jupyter Notebooks that demonstrate how to programmatically manage ArcGIS Online Hosted Feature Layers — updating domains, configuring views, adding tables, and building relationships — without ever needing to republish your data.

---

## Prerequisites

- Python 3.x
- [ArcGIS API for Python](https://developers.arcgis.com/python/) (`arcgis`)
- `pandas`
- An ArcGIS Online account with administrator privileges
- Jupyter Notebook or JupyterLab

Install dependencies:
```bash
pip install arcgis pandas
```

---

## Workshop Scripts

Run the notebooks in order. Each builds on the environment created by the previous one.

### Script 1 — Create Workshop Environment
Connects to ArcGIS Online and clones the necessary items from the source organization into a new `WLIA HFL Workshop` folder in your account.

**Clones:**
- Trees feature layer
- Tree Inspection layer
- Wolf Lodge Trees Public View
- Trees Web Map

### Script 2 — Update HFL Domains
Reads a list of 50 tree species from [`TreeCommonNames.csv`](TreeCommonNames.csv) and applies a coded value domain to the `CommonName` field on the Trees feature layer, enabling standardized dropdown selection in field collection apps.

### Script 3 — Update Views / Joined Views with SourceSchema
Finds all View Services in your organization that reference the Trees feature layer and sets `sourceSchemaChangesAllowed = true` on each, so views automatically reflect schema changes without needing to be recreated.

### Script 4 — Add Table to a Hosted Feature Service
Copies the Tree Inspection table structure from a template feature service and appends it to the Trees Hosted Feature Service, making it accessible in the ArcGIS Online UI.

**Table fields:** `OBJECTID`, `AshBorer`, `Condition`, `TreeGUID`

### Script 5 — Create Relationships
Establishes a one-to-many relationship between the Trees layer and the Tree Inspection table using `GlobalID` → `TreeGUID` as the key fields, enabling related record queries in the field and in web apps.

---

## Data Model

```
Trees (Layer 0)
├── OBJECTID
├── CommonName  ← domain applied in Script 2
├── Diameter
├── Valuation
└── GlobalID ──────────────────────┐
                                   │ 1:many relationship (Script 5)
Tree Inspection (Table 1)          │
├── OBJECTID                       │
├── AshBorer                       │
├── Condition                      │
└── TreeGUID ──────────────────────┘
```

---

## Repository Contents

| File | Description |
|---|---|
| `Script1.ipynb` | Creates the workshop environment |
| `Script2.ipynb` | Updates HFL domains |
| `Script3.ipynb` | Enables sourceSchema on views |
| `Script4.ipynb` | Adds a table to a Hosted Feature Service |
| `Script5.ipynb` | Creates layer/table relationships |
| `TreeCommonNames.csv` | Domain reference — 50 tree species (Label + Code) |
| `Python Refresher before the ArcGIS API for Python.pdf` | Pre-workshop Python reference |
| `WLIA Workshop Presentation.pdf` | Slide deck for the workshop |

---

## Additional Resources

- [ArcGIS API for Python Documentation](https://developers.arcgis.com/python/)
- [ArcGIS Online Help — Hosted Feature Layers](https://doc.arcgis.com/en/arcgis-online/manage-data/hosted-web-layers.htm)
