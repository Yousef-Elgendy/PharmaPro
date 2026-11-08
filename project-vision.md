# PharmaPro Vision — Pharmacy Sales & Inventory Management System

> **Project Name:** PharmaPro
> **Track:** DEPI Graduation Project (.NET Full-Stack)
> **Author:** Team 1
> **Date:** November 2026
> **Repository:** PharmaPro

## 1. Overview
A responsive web application that serves as the operational control center of a pharmacy. It manages medicines (products), categories, suppliers, stock levels, and sales, giving staff an accurate, real-time picture of what is in stock and what has been sold.

## 2. Problem Statement
Small and medium pharmacies often track stock on paper or in spreadsheets. This leads to:
- Selling expired or unavailable medicines
- Not knowing when stock is running low
- No traceability of who received, adjusted, or sold what
- Slow checkout and inconsistent pricing

## 3. Vision Statement
> Give every pharmacy a reliable, easy-to-use system that tracks medicine from the moment it is received from a supplier until the moment it is sold to a customer, while making expired-medicine sales impossible.

## 4. Goals
1. Provide a complete, trustworthy workflow: Supplier -> Stock-in (Batch) -> Inventory -> Sale.
2. Guarantee safety through batch and expiry-date tracking (FEFO: First Expired, First Out).
3. Provide a fast POS experience with search by name/barcode and visual product cards (images).
4. Enforce role-based access so each employee sees only what they need.
5. Give management a dashboard with sales totals, low-stock and near-expiry alerts.

## 5. Target Users
| Role | Primary Need |
|------|--------------|
| Administrator | Full control: users, products, suppliers, reports |
| Sales Clerk (Pharmacist) | Sell quickly and accurately, see available products |
| Stock Manager | Record incoming stock and adjustments with full traceability |

## 6. Scope Summary
- Product & Category catalog (CRUD, images, unique SKU)
- Supplier management
- Inventory with Batches (batch number + expiry date) and Stock Movement logs
- Sales / POS with business-rule validation and automatic stock update
- Dashboard (product stats, low-stock alerts, total sales)
- Authentication and role-based access control

## 7. Technology Stack
- Frontend: HTML5, CSS3, JavaScript (fetch/AJAX)
- Backend: C# with ASP.NET Core Web API
- Database: Microsoft SQL Server (relational, normalized)
- Testing: xUnit
- Workflow: GitHub, `main` / `develop` branches, Pull Requests

## 8. Success Criteria
- A sale can never exceed available non-expired stock.
- Every stock change is traceable to a user, date, and reason.
- SKU uniqueness is enforced.
- All critical business rules are covered by unit tests.
- Each role can only access its permitted features.

## 9. Out of Scope (initial release)
Online ordering, customer accounts, insurance claims, payment gateway integration, multi-branch support.
