---
title: "Data Sources & Refresh Schedule"
description: "Information about data sources and their refresh schedules"
category: "Main"
order: 2
breadcrumb: []
---

# Data Sources & Refresh Schedule

## Overview

This page documents all data sources feeding into the AB Texel reporting system, their refresh schedules, and data quality information.

## Data Sources

### Primary Systems

| System | Description | Owner | Refresh Frequency |
|--------|-------------|-------|-------------------|
| CBS | Central Business System | IT | Daily at 02:00 AM |
| BigMile | Fleet Management | Fleet Ops | Real-time / Hourly |
| Financial System | Accounting & GL | Finance | Daily at 04:00 AM |
| Customer Database | Client Information | Sales | As needed |

## Refresh Schedule

### Daily Refreshes
- **02:00 AM** - CBS data import
- **04:00 AM** - Financial system sync
- **06:00 AM** - Report generation begins

### Hourly Refreshes
- **BigMile Fleet data** - Updated every hour during business hours (06:00 AM - 10:00 PM)

### Real-time Feeds
- **System monitoring and anomaly detection** - Continuous

## Data Quality & SLA

### Service Level Agreements (SLA)

| Report | Availability | Recovery Time |
|--------|-------------|----------------|
| Financial Operations | 99.5% | 4 hours |
| Fleet Hours | 99.0% | 8 hours |
| Customer Reporting | 99.5% | 4 hours |
| Fuel Reporting | 98.5% | 12 hours |

### Known Data Delays

- Financial reporting may lag source system by 24 hours
- Fleet data includes 15-minute processing delay
- Customer data updated upon request or daily batch

## Data Lineage

For detailed information on how data flows through the system, see [System Integration](06-system-integration.md).

---

**Last Updated:** June 2024  
**Next:** [Access & Permissions](03-access-permissions.md)
