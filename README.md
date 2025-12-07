# 30 Data Engineering Projects: Beginner to Expert
## Complete Learning Path with Tools & Concepts

---

## 🟢 Beginner (Projects 1-10)
*Focus: SQL mastery, Python for data, basic ETL, file formats, scheduling*

---

### 1. CSV to PostgreSQL Loader
**What You Build:** Script to read CSV files, clean data, load into PostgreSQL

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Languages | Python, SQL |
| Libraries | pandas, psycopg2 or SQLAlchemy |
| Database | PostgreSQL |
| Concepts | Schema design, data types, bulk inserts |

**Tasks:**
- Handle encoding issues (UTF-8, Latin-1)
- Implement data type inference
- Handle NULL values and duplicates
- Create indexes for query performance
- Log success/failure counts

---

### 2. Web Scraping Pipeline
**What You Build:** Scrape product data from e-commerce sites, store structured

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Libraries | BeautifulSoup, Scrapy, requests |
| Storage | PostgreSQL + JSON files |
| Concepts | Rate limiting, robots.txt, incremental loads |

**Tasks:**
- Respect rate limits and robots.txt
- Handle pagination and retries
- Store raw HTML (bronze) and parsed data (silver)
- Schedule daily runs with cron
- Detect and handle site structure changes

---

### 3. API Data Collector
**What You Build:** Pull data from REST APIs (weather, stocks, social media)

**Skills & Tools:**
| Category | Details |
|----------|---------|
| APIs | OpenWeatherMap, Alpha Vantage, Twitter |
| Libraries | requests, aiohttp for async |
| Storage | PostgreSQL, JSON files |
| Concepts | API pagination, rate limits, authentication |

**Tasks:**
- Handle API keys securely (environment variables)
- Implement exponential backoff for failures
- Store API responses with timestamps
- Track API quota usage
- Build incremental data fetching

---

### 4. File Format Converter
**What You Build:** Convert between CSV, JSON, Parquet, Avro formats

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Libraries | pandas, pyarrow, fastavro |
| Formats | CSV, JSON, Parquet, Avro |
| Concepts | Columnar vs row storage, compression, schemas |

**Tasks:**
- Compare file sizes across formats
- Benchmark read/write speeds
- Handle nested JSON to flat Parquet
- Implement schema evolution (adding columns)
- Test with datasets from 1MB to 10GB

---

### 5. Database Backup & Restore System
**What You Build:** Automated backup system with point-in-time recovery

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Tools | pg_dump, pg_restore, boto3 |
| Storage | Local disk, AWS S3 |
| Concepts | Full vs incremental backups, retention policies |

**Tasks:**
- Schedule daily full backups
- Implement backup rotation (keep last 7 days)
- Upload to S3 with lifecycle policies
- Test restore procedures
- Monitor backup success/failure

---

### 6. Data Quality Checker
**What You Build:** Framework to validate data against defined rules

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Libraries | Great Expectations, pandas, pydantic |
| Concepts | Data contracts, schema validation, profiling |

**Tasks:**
- Check for nulls, duplicates, range violations
- Validate referential integrity
- Profile data distributions
- Generate data quality reports
- Alert on quality failures

---

### 7. Log Parser & Analyzer
**What You Build:** Parse application logs, extract metrics, store for analysis

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Libraries | regex, pandas, click (CLI) |
| Log Types | Apache/Nginx access logs, application logs |
| Storage | PostgreSQL, Elasticsearch |

**Tasks:**
- Parse various log formats (Apache, JSON, custom)
- Extract timestamps, IPs, status codes, response times
- Aggregate metrics (requests/min, error rates)
- Handle log rotation and compressed files
- Build CLI tool for ad-hoc analysis

---

### 8. SQL Query Performance Analyzer
**What You Build:** Tool to analyze and optimize slow queries

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Database | PostgreSQL |
| Concepts | EXPLAIN ANALYZE, indexes, query plans |

**Tasks:**
- Capture slow queries from pg_stat_statements
- Parse and visualize query plans
- Recommend index creation
- Compare before/after performance
- Track query performance over time

---

### 9. Dimensional Data Model
**What You Build:** Star schema data warehouse for retail sales data

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Concepts | Star schema, fact tables, dimension tables, SCD |
| Database | PostgreSQL or DuckDB |
| Modeling | Kimball methodology |

**Tables to Build:**
- fact_sales (measures: quantity, amount, discount)
- dim_product (attributes: name, category, brand)
- dim_customer (attributes: name, segment, location)
- dim_date (attributes: day, week, month, quarter, year)
- dim_store (attributes: name, region, type)

**Tasks:**
- Implement Type 1 and Type 2 slowly changing dimensions
- Create surrogate keys
- Build ETL to populate from source system
- Write analytical queries (sales by region, YoY growth)

---

### 10. Scheduled ETL with Cron
**What You Build:** End-to-end pipeline with scheduling, logging, monitoring

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Scheduler | cron (Linux) or Task Scheduler (Windows) |
| Monitoring | Email alerts, log files |
| Concepts | Idempotency, failure handling, logging |

**Tasks:**
- Create idempotent ETL scripts
- Implement logging with rotation
- Send email alerts on failure
- Create monitoring dashboard (simple HTML)
- Handle partial failures gracefully

---

## 🟡 Intermediate (Projects 11-20)
*Focus: Orchestration, cloud services, streaming basics, data modeling*

---

### 11. Airflow DAG Pipeline
**What You Build:** Multi-step ETL orchestrated with Apache Airflow

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Orchestrator | Apache Airflow |
| Concepts | DAGs, operators, sensors, XComs, connections |
| Infrastructure | Docker, docker-compose |

**DAG Structure:**
```
check_source_ready → extract_api_data → validate_data 
    → transform_data → load_to_warehouse → run_quality_checks
    → notify_success
```

**Tasks:**
- Set up Airflow with Docker
- Create custom operators
- Implement task dependencies and branching
- Use sensors to wait for files/conditions
- Build failure callbacks and alerts

---

### 12. Cloud Data Lake (AWS)
**What You Build:** S3-based data lake with proper organization

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Services | AWS S3, IAM, Glue Catalog |
| Format | Parquet with partitioning |
| Concepts | Bronze/Silver/Gold layers, partitioning strategies |

**Architecture:**
```
s3://data-lake/
├── bronze/          # Raw data as-is
│   └── source=api/year=2024/month=01/
├── silver/          # Cleaned, typed
│   └── domain=sales/year=2024/month=01/
└── gold/            # Aggregated, business-ready
    └── reports/daily_sales/
```

**Tasks:**
- Implement lifecycle policies (move old data to Glacier)
- Set up Glue Crawler for schema discovery
- Partition by date for efficient querying
- Implement proper IAM roles
- Enable versioning and access logging

---

### 13. dbt Transformation Project
**What You Build:** Layered transformation project with dbt

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Tool | dbt (data build tool) |
| Database | PostgreSQL, Snowflake, or BigQuery |
| Concepts | Staging, intermediate, marts, testing, docs |

**Model Structure:**
```
models/
├── staging/           # 1:1 with sources, renaming/casting
│   ├── stg_orders.sql
│   └── stg_customers.sql
├── intermediate/      # Business logic, joins
│   └── int_orders_enriched.sql
└── marts/            # Final tables for BI
    ├── dim_customers.sql
    └── fct_orders.sql
```

**Tasks:**
- Write staging models with source freshness checks
- Implement incremental models
- Add dbt tests (unique, not_null, relationships)
- Generate documentation site
- Set up CI/CD for dbt runs

---

### 14. Change Data Capture (CDC) Pipeline
**What You Build:** Capture database changes and replicate in near real-time

**Skills & Tools:**
| Category | Details |
|----------|---------|
| CDC Tool | Debezium |
| Message Queue | Apache Kafka |
| Database | PostgreSQL (source), PostgreSQL (target) |

**Tasks:**
- Set up Debezium PostgreSQL connector
- Capture INSERT, UPDATE, DELETE operations
- Handle schema changes
- Implement exactly-once delivery
- Monitor replication lag

---

### 15. Kafka Streaming Basics
**What You Build:** Real-time event processing pipeline

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Streaming | Apache Kafka, kafka-python or confluent-kafka |
| Concepts | Topics, partitions, consumers, producers, offsets |

**Tasks:**
- Set up Kafka cluster with Docker
- Create producers for event generation
- Build consumers with different consumer groups
- Implement message serialization (Avro with Schema Registry)
- Monitor lag and throughput
- Handle consumer rebalancing

---

### 16. Data Warehouse on BigQuery/Snowflake
**What You Build:** Complete cloud data warehouse with ingestion

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Platform | BigQuery or Snowflake |
| Concepts | Clustering, partitioning, materialized views |
| Ingestion | Fivetran/Airbyte or custom scripts |

**Tasks:**
- Design schema with clustering keys
- Implement time-based partitioning
- Create materialized views for dashboards
- Set up roles and access controls
- Monitor costs and optimize queries
- Build incremental loading

---

### 17. Spark Batch Processing
**What You Build:** Large-scale data processing with PySpark

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Framework | Apache Spark (PySpark) |
| Deployment | Local, Docker, or Databricks Community |
| Concepts | RDDs, DataFrames, transformations, actions |

**Tasks:**
- Process 10GB+ dataset (taxi trips, web logs)
- Implement joins across large datasets
- Use window functions for running totals
- Optimize with partitioning and caching
- Write results to Parquet with partitioning
- Tune Spark configurations for performance

---

### 18. Metadata & Data Catalog
**What You Build:** Searchable catalog of all data assets

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Tools | Apache Atlas, Amundsen, or DataHub |
| Concepts | Data lineage, schema registry, data discovery |

**Tasks:**
- Ingest metadata from databases and data lakes
- Track data lineage (source → transformations → output)
- Implement search by column name, table, owner
- Document data definitions and ownership
- Show column-level lineage

---

### 19. Python Data Pipeline Framework
**What You Build:** Reusable framework for building pipelines

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Libraries | Custom Python package |
| Patterns | Factory pattern, dependency injection |
| Quality | pytest, mypy, pre-commit hooks |

**Framework Components:**
```python
# Extractors
class PostgresExtractor(BaseExtractor): ...
class S3Extractor(BaseExtractor): ...

# Transformers  
class DataCleanerTransformer(BaseTransformer): ...

# Loaders
class BigQueryLoader(BaseLoader): ...

# Pipeline
pipeline = Pipeline([
    PostgresExtractor(config),
    DataCleanerTransformer(rules),
    BigQueryLoader(destination)
])
pipeline.run()
```

**Tasks:**
- Build abstract base classes
- Implement configuration management
- Add comprehensive logging
- Write unit and integration tests
- Package for pip installation

---

### 20. Real-Time Dashboard Pipeline
**What You Build:** Streaming data to live dashboard

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Streaming | Kafka or Kinesis |
| Processing | Kafka Streams or Flink SQL |
| Visualization | Grafana, Apache Superset |
| Storage | InfluxDB or TimescaleDB |

**Tasks:**
- Generate simulated event stream
- Aggregate in real-time (counts, averages per minute)
- Store time-series data
- Build live-updating Grafana dashboard
- Alert on anomalies (spike in errors)

---

## 🟠 Advanced (Projects 21-26)
*Focus: Scale, reliability, advanced streaming, data mesh, ML pipelines*

---

### 21. Lakehouse Architecture
**What You Build:** Delta Lake / Iceberg based lakehouse

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Format | Delta Lake or Apache Iceberg |
| Features | ACID transactions, time travel, schema evolution |
| Query Engine | Spark, Trino, or Dremio |

**Tasks:**
- Set up Delta Lake on S3
- Implement MERGE (upserts) operations
- Use time travel for debugging
- Handle schema evolution gracefully
- Compact small files (bin-packing)
- Implement Z-ordering for query optimization

---

### 22. Stream Processing with Flink
**What You Build:** Complex event processing application

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Framework | Apache Flink (PyFlink or Java) |
| Concepts | Event time, watermarks, windows, state |

**Use Cases:**
- Sessionization (group events by user session)
- Fraud detection (pattern matching)
- Real-time aggregations with late data handling

**Tasks:**
- Implement event-time processing with watermarks
- Create tumbling and sliding windows
- Handle late arriving data
- Manage stateful operations with checkpoints
- Implement exactly-once semantics

---

### 23. Data Mesh Implementation
**What You Build:** Domain-oriented data ownership architecture

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Concepts | Data products, domain ownership, self-serve platform |
| Tools | dbt, Airflow, DataHub, Terraform |

**Domain Structure:**
```
domains/
├── sales/
│   ├── data-products/
│   │   ├── orders/          # Full data product
│   │   │   ├── dbt/
│   │   │   ├── airflow/
│   │   │   └── metadata.yaml
│   │   └── customers/
│   └── team.yaml
├── marketing/
│   └── data-products/
│       └── campaigns/
└── platform/               # Self-serve infrastructure
    ├── terraform/
    └── templates/
```

**Tasks:**
- Define data product standards
- Implement data contracts between domains
- Build self-serve infrastructure templates
- Create federated governance model
- Implement cross-domain lineage

---

### 24. ML Feature Store
**What You Build:** Centralized feature management for ML

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Tools | Feast, Tecton, or custom |
| Storage | Online (Redis) + Offline (Parquet/BigQuery) |
| Concepts | Feature engineering, point-in-time correctness |

**Tasks:**
- Define feature definitions in code
- Implement batch feature computation
- Set up online serving with low latency (<10ms)
- Handle point-in-time joins for training
- Version features and track lineage
- Monitor feature drift

---

### 25. Data Pipeline Testing Framework
**What You Build:** Comprehensive testing for data pipelines

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Testing | pytest, Great Expectations, dbt tests |
| Concepts | Unit, integration, contract, regression testing |

**Test Types:**
```
tests/
├── unit/                    # Transform logic
│   └── test_transformations.py
├── integration/             # End-to-end
│   └── test_pipeline_e2e.py
├── contract/               # Schema contracts
│   └── test_output_schema.py
├── data_quality/           # Great Expectations
│   └── expectations/
└── regression/             # Compare outputs
    └── test_output_regression.py
```

**Tasks:**
- Mock external dependencies
- Test with sample datasets
- Implement schema contract tests
- Build regression tests comparing outputs
- Integrate tests into CI/CD

---

### 26. Infrastructure as Code for Data Platform
**What You Build:** Terraform-managed cloud data infrastructure

**Skills & Tools:**
| Category | Details |
|----------|---------|
| IaC | Terraform |
| Cloud | AWS, GCP, or Azure |
| CI/CD | GitHub Actions, GitLab CI |

**Infrastructure to Provision:**
```hcl
# AWS Example
module "data_lake" {
  # S3 buckets with lifecycle policies
}

module "data_warehouse" {
  # Redshift cluster with proper networking
}

module "airflow" {
  # MWAA or self-hosted on EKS
}

module "kafka" {
  # MSK cluster
}

module "networking" {
  # VPC, subnets, security groups
}
```

**Tasks:**
- Modularize infrastructure components
- Implement state management (remote backend)
- Set up different environments (dev/staging/prod)
- Implement proper secrets management
- Create CI/CD for infrastructure changes

---

## 🔴 Expert (Projects 27-30)
*Focus: Production systems, cost optimization, governance, complete platforms*

---

### 27. Real-Time Fraud Detection System
**What You Build:** Production streaming system with ML integration

**Architecture:**
```
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│ Events  │───▶│  Kafka  │───▶│  Flink  │───▶│ Action  │
└─────────┘    └─────────┘    └─────────┘    └─────────┘
                                   │
                              ┌────┴────┐
                              │ ML Model│
                              │ (Redis) │
                              └─────────┘
```

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Streaming | Kafka, Flink |
| ML Serving | Redis ML, Seldon, or custom |
| Monitoring | Prometheus, Grafana, PagerDuty |

**Tasks:**
- Process 100K+ events/second
- Implement feature computation in real-time
- Integrate ML model for scoring
- Handle model updates without downtime
- Alert on detected fraud
- Store all decisions for audit

---

### 28. Multi-Region Data Replication
**What You Build:** Globally distributed data system with consistency

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Databases | PostgreSQL with logical replication, CockroachDB |
| Patterns | Active-active, conflict resolution |
| Cloud | Multi-region AWS/GCP setup |

**Tasks:**
- Set up cross-region replication
- Handle conflict resolution strategies
- Implement read/write routing
- Monitor replication lag globally
- Test failover scenarios
- Optimize for latency vs consistency

---

### 29. Data Governance & Compliance Platform
**What You Build:** Complete governance system for regulated industry

**Skills & Tools:**
| Category | Details |
|----------|---------|
| Tools | Apache Atlas, Collibra, or custom |
| Compliance | GDPR, CCPA, HIPAA patterns |
| Security | Column-level encryption, masking, audit logs |

**Components:**
- **Data Classification:** Auto-tag PII, PHI, financial data
- **Access Control:** Attribute-based access control (ABAC)
- **Data Masking:** Dynamic masking for non-prod
- **Audit Logging:** Complete access audit trail
- **Retention:** Automated data lifecycle management
- **Consent Management:** Track user consent for data usage

**Tasks:**
- Implement automated PII detection
- Build approval workflows for data access
- Create audit reports for compliance
- Implement right-to-deletion (GDPR)
- Monitor data access patterns for anomalies

---

### 30. Enterprise Data Platform
**What You Build:** Complete, production-ready data platform

**Architecture:**
```
┌────────────────────────────────────────────────────────────┐
│                     DATA SOURCES                           │
│  [Databases] [APIs] [Files] [Streams] [SaaS Apps]         │
└─────────────────────────┬──────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────┐
│                    INGESTION LAYER                         │
│  [Airbyte/Fivetran] [Kafka Connect] [Custom Connectors]   │
└─────────────────────────┬──────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────┐
│                     STORAGE LAYER                          │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐               │
│  │ Bronze  │───▶│ Silver  │───▶│  Gold   │  [Delta Lake] │
│  │  (Raw)  │    │(Cleaned)│    │ (Marts) │               │
│  └─────────┘    └─────────┘    └─────────┘               │
└─────────────────────────┬──────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────┐
│                  PROCESSING LAYER                          │
│  [Spark] [dbt] [Flink] [Airflow Orchestration]            │
└─────────────────────────┬──────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────┐
│                   SERVING LAYER                            │
│  [Trino/Presto] [Snowflake] [Feature Store] [APIs]        │
└─────────────────────────┬──────────────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────────────┐
│                  CONSUMPTION LAYER                         │
│  [BI Tools] [ML Platforms] [Applications] [Analysts]      │
└────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────┐
│                   CROSS-CUTTING CONCERNS                   │
│  [Data Catalog] [Lineage] [Quality] [Security] [Costs]    │
└────────────────────────────────────────────────────────────┘
```

**Complete Feature Set:**

| Component | Implementation |
|-----------|---------------|
| Ingestion | Airbyte for batch, Kafka for streaming |
| Storage | S3 + Delta Lake |
| Transformation | dbt + Spark |
| Orchestration | Airflow on Kubernetes |
| Serving | Trino for federation, Redis for features |
| Catalog | DataHub |
| Quality | Great Expectations |
| Governance | Apache Atlas + custom |
| Monitoring | Prometheus + Grafana |
| Cost Management | Custom dashboards + alerts |
| IaC | Terraform + Helm |
| CI/CD | GitHub Actions |

**Tasks:**
- Deploy entire platform with Terraform
- Implement complete CI/CD for all components
- Create self-service onboarding for new data sources
- Build cost allocation and chargeback
- Implement comprehensive monitoring and alerting
- Create runbooks for common operations
- Document architecture decisions (ADRs)
- Train team on platform usage

---

## Complete Skills Checklist

### Programming & SQL
- [ ] Python (pandas, PySpark, async)
- [ ] SQL (window functions, CTEs, optimization)
- [ ] Bash scripting
- [ ] Basic Java/Scala (for JVM tools)

### Databases
- [ ] PostgreSQL (advanced features)
- [ ] Cloud warehouses (Snowflake/BigQuery/Redshift)
- [ ] NoSQL (MongoDB, Cassandra basics)
- [ ] Time-series (InfluxDB/TimescaleDB)

### Big Data & Processing
- [ ] Apache Spark (batch)
- [ ] Apache Flink (streaming)
- [ ] Apache Kafka (messaging)
- [ ] Hadoop ecosystem basics

### Orchestration & Workflow
- [ ] Apache Airflow
- [ ] dbt
- [ ] Dagster or Prefect (alternatives)

### Cloud Platforms
- [ ] AWS (S3, Glue, Redshift, EMR, Kinesis)
- [ ] GCP (BigQuery, Dataflow, Pub/Sub)
- [ ] Azure (Data Factory, Synapse)

### DevOps & Infrastructure
- [ ] Docker & Kubernetes
- [ ] Terraform
- [ ] CI/CD pipelines
- [ ] Monitoring (Prometheus, Grafana)

### Data Modeling & Quality
- [ ] Dimensional modeling (Kimball)
- [ ] Data vault basics
- [ ] Great Expectations
- [ ] dbt testing

### Governance & Catalog
- [ ] Data lineage concepts
- [ ] Metadata management
- [ ] Data privacy (GDPR, CCPA)

---

## Learning Tips

1. **Start with SQL mastery** — It's used everywhere
2. **Build end-to-end first** — Understanding full flow beats deep expertise in one area
3. **Use real datasets** — Kaggle, public APIs, government data
4. **Containerize everything** — Docker makes learning tools easier
5. **Track costs** — Cloud bills teach optimization fast
6. **Read postmortems** — Learn from production failures
7. **Contribute to open source** — Great for learning and networking
8. **Get cloud certifications** — AWS/GCP DE certs validate knowledge

---

## Suggested Timeline

| Phase | Projects | Duration |
|-------|----------|----------|
| Foundation | 1-10 | 3-4 months |
| Intermediate | 11-20 | 4-6 months |
| Advanced | 21-26 | 4-6 months |
| Expert | 27-30 | 6-12 months |

**Total: 18-28 months to expert level with consistent practice**
