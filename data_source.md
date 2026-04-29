# Business Data Sources Review

This document provides a technical analysis of the primary data source categories utilized in modern Business Intelligence (BI) architectures. Identifying and characterizing these sources is a critical first step in the ETL (Extract, Transform, Load) process, as the structure, velocity, and integrity of source data directly dictate the design of the downstream data warehouse.

## 1. Transactional Databases (OLTP)
The primary system of record for most enterprises is the Online Transactional Processing (OLTP) database. These are typically relational database management systems (RDBMS) such as PostgreSQL, MySQL, or Microsoft SQL Server.

Technical Characteristics: These sources are highly normalized to reduce data redundancy and adhere strictly to ACID (Atomicity, Consistency, Isolation, Durability) properties, ensuring reliable transaction processing.

Business Context: They house core operational data from ERP (Enterprise Resource Planning) and CRM (Customer Relationship Management) systems, including sales transactions, inventory levels, and customer records.

BI Implementation: Because OLTP systems are optimized for fast writes, querying them directly for complex analytics can degrade production performance. Consequently, data is typically extracted using incremental loading techniques to a staging area before being transformed into a multi-dimensional model.

## 2. Flat Files
Despite the prevalence of structured databases, a significant volume of organizational data remains stored in decoupled Flat Files. These are frequently used for manual reporting, department-level tracking, or as output from legacy systems.

Common Formats: Comma-Separated Values (CSV), Excel Workbooks (.xlsx), and semi-structured formats like JSON and XML.

Technical Implications: Unlike databases, flat files lack built-in schema enforcement. This requires the BI developer to implement robust schema-on-read strategies and data validation rules during ingestion to handle null values, inconsistent formatting, or incorrect data types.

Academic Observation: These sources often create "Data Silos," where critical information is isolated from the central enterprise data strategy, necessitating a unified ingestion layer to ensure a "single version of the truth."

## 3. APIs (Application Programming Interfaces)
Modern BI pipelines increasingly ingest data from cloud-native environments and third-party SaaS (Software as a Service) platforms via RESTful APIs.

Data Ingestion: Data is typically retrieved in JSON payloads. This allows the business to integrate external data—such as marketing metrics from Google Ads, social media sentiment, or financial data from payment gateways—directly into their analytical models.

Engineering Constraints: Implementing API-based ingestion introduces unique technical challenges, including Rate Limiting (server-side request throttling), OAuth2 Authentication protocols, and the need for pagination logic to handle large datasets efficiently.

## 4. Streaming Data
For businesses requiring real-time operational intelligence, Streaming Data sources provide high-velocity information that must be processed as it is generated, rather than in scheduled batches.

Source Examples: Internet of Things (IoT) sensor feeds, web server logs (clickstream data), and real-time financial market updates.

Infrastructure: Unlike traditional batch processing, streaming requires event brokers like Apache Kafka or Amazon Kinesis to buffer and sequence data before it is ingested into a Data Lake or a real-time analytics engine.

Analytical Value: This allows for Prescriptive Analytics, such as real-time fraud detection or dynamic pricing, where the window of opportunity for action is measured in seconds rather than days.