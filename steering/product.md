# Product Overview

This is a Human Resource Management (HRM) system with BPO (Business Process Outsourcing) capabilities, built for organizations to manage their workforce.

## Core Modules

- **Employee Management** — profiles, roles, permissions, organizational hierarchy
- **Attendance** — punch in/out, daily logs, geolocation tracking, attendance requests/approvals
- **Leave Management** — requests, calendar, allowances, approvals
- **Overtime (OT)** — OT requests, records, summaries with multipliers (x1.5, x2, x3)
- **Contracts** — contract tracking with expiration notifications
- **Payroll & Salary** — salary management, payslip generation (PDF)
- **Assets** — company asset tracking and assignment
- **Working Shifts** — shift scheduling and management
- **Holidays** — holiday calendar management
- **Announcements** — internal communications
- **Role-Based Access Control** — granular permission system (admin, manager, employee)

## Multi-Tenancy

The system supports multiple organizations (tenants) with isolated data and tenant-specific routes/models.

## Localization

Supports English, Vietnamese, and Japanese. Translation files live in `src/resources/lang/`.
