---
title: "System Integration (CBS & BigMile)"
description: "Overview of system integrations and data flows"
category: "Main"
order: 6
breadcrumb: []
---

# System Integration (CBS & BigMile)

## Overview

AB Texel's reporting system integrates with multiple business systems. This document details the integration architecture, data flows, and technical specifications.

## Integrated Systems

### CBS (Central Business System)

**Purpose:** Core financial and operational data  
**Data Updated:** Daily at 02:00 AM  
**Key Data Points:**
- Financial transactions
- Invoice and payment data
- Customer master data
- Product catalog

**Integration Method:** API / Database sync  
**Contact:** IT Department

### BigMile (Fleet Management System)

**Purpose:** Fleet operations and tracking  
**Data Updated:** Real-time / Hourly  
**Key Data Points:**
- Vehicle locations and status
- Fuel consumption
- Maintenance records
- Driver hours
- Route information

**Integration Method:** Real-time API / Webhooks  
**Contact:** Fleet Operations

## Data Flow Architecture

```
CBS → Extract Layer → Transform → Load → Data Warehouse → Reporting Layer
BigMile → Extract Layer → Transform → Load → Data Warehouse → Reporting Layer
```

## Integration Specifications

### CBS Integration
- **Protocol:** HTTPS REST API
- **Authentication:** API Key + OAuth 2.0
- **Update Frequency:** Daily batch
- **Error Handling:** Automatic retry with alerts
- **Data Validation:** 95%+ accuracy required

### BigMile Integration
- **Protocol:** HTTPS REST API + Webhooks
- **Authentication:** API Key + JWT Token
- **Update Frequency:** Real-time / Hourly
- **Error Handling:** Queue-based with dead-letter handling
- **Data Validation:** Real-time validation with alerts

## Maintenance & Support

### System Downtime
- Planned maintenance: Weekends 2:00 AM - 4:00 AM EST
- Emergency maintenance: As needed with user notification
- Contact: IT Help Desk

### Data Quality Issues
- Automated anomaly detection with alerts
- Daily data quality reports
- Manual validation on request
- Contact: Data Administration team

## Troubleshooting

### Common Issues
1. **Missing data** - Check CBS/BigMile system status
2. **Delayed refresh** - Review integration logs
3. **Incorrect values** - Validate source system entries

See [FAQs](09-faqs.md) or [Contact & Support](10-contact-support.md) for more help.

---

**Last Updated:** June 2024  
**Previous:** [Reports & Client Reporting](client-reporting/00-client-reporting.md)
