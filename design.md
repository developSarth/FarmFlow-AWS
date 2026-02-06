# Design Document: FarmFlow App

## Overview

FarmFlow is a web-based application designed to help organic multilayer farmers survive and thrive through systematic planning of cash-flow, labor, and direct selling. The system provides a data-driven approach to farm design by generating ecological blueprints, tracking monthly survival income, identifying dry periods, and connecting farmers with organic-only buyers.

The application follows a dual-profile architecture with a React-based frontend and a RESTful API backend. Data persistence is handled through a relational database, and the system emphasizes reality-based inputs, honest risk assessment, and trust-building between farmers and organic retailers.

**Infrastructure:** This project is powered by AWS (Amazon Web Services) sponsorship, providing enterprise-grade cloud infrastructure with enhanced reliability, security, and scalability.

---

## System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (React)                         │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │   Farmer     │  │   Retailer   │  │   Farm       │    │
│  │   Profile    │  │   Profile    │  │   Design     │    │
│  │  Component   │  │  Component   │  │  Component   │    │
│  └──────────────┘  └──────────────┘  └──────────────┘    │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │  Cash-Flow   │  │   Market     │  │  Integrity   │    │
│  │   Tracker    │  │  Discovery   │  │   Score      │    │
│  │  Component   │  │  Component   │  │  Component   │    │
│  └──────────────┘  └──────────────┘  └──────────────┘    │
└─────────────────────────────────────────────────────────────┘
                            |
                    REST API (JSON)
                            |
┌─────────────────────────────────────────────────────────────┐
│                  Backend API Server                         │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │   Farmer     │  │   Farm       │  │  Cash-Flow   │    │
│  │   Service    │  │   Design     │  │   Service    │    │
│  │              │  │   Service    │  │              │    │
│  └──────────────┘  └──────────────┘  └──────────────┘    │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │  Retailer    │  │    Auth      │  │  Integrity   │    │
│  │   Service    │  │   Service    │  │   Service    │    │
│  │              │  │              │  │              │    │
│  └──────────────┘  └──────────────┘  └──────────────┘    │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐                       │
│  │   Market     │  │  Risk/Dry    │                       │
│  │  Matching    │  │   Period     │                       │
│  │   Service    │  │   Service    │                       │
│  └──────────────┘  └──────────────┘                       │
└─────────────────────────────────────────────────────────────┘
                            |
                         Database
                            |
┌─────────────────────────────────────────────────────────────┐
│              PostgreSQL / MySQL Database                    │
│                                                             │
│  Tables: Farmers, Retailers, Farms, Crops, Contracts,      │
│  CashFlow, Integrity, ProductionCalendar, MarketMatches    │
└─────────────────────────────────────────────────────────────┘
```

### Component Breakdown

**Frontend Layer:**
- React-based single-page application
- Component-based architecture for reusability
- State management for user sessions and data
- Responsive design for mobile and desktop
- Local language support

**API Layer:**
- RESTful API with JSON communication
- JWT-based authentication
- Request validation and sanitization
- Error handling and logging
- Rate limiting and security

**Backend Services:**
- Modular service architecture
- Business logic separation
- Database abstraction layer
- External integrations (SMS, maps)

**Database Layer:**
- Relational database for structured data
- Normalized schema design
- Indexing for performance
- Backup and recovery mechanisms

---

## User Workflows

### Farmer Journey (End-to-End)

**Step 1: Onboarding**
1. Register with mobile number
2. Complete farmer profile (reality-based inputs)
3. Submit land and resource details
4. Indicate current farming stage

**Step 2: Farm Design**
1. System generates 3-zone blueprint
2. Review visual farm map
3. Read zone-wise explanations
4. Adjust preferences (optional)
5. Finalize and save design

**Step 3: Risk Assessment**
1. System calculates dry period
2. Review month-by-month projection
3. See risk warnings
4. Review seasonal survival plan
5. Understand income gaps

**Step 4: Implementation & Tracking**
1. Follow planting schedule
2. Record weekly/monthly harvests
3. Enter sales and prices
4. Monitor cash-flow tracker
5. Receive alerts and suggestions

**Step 5: Building Integrity**
1. System auto-tracks organic practices
2. Integrity score builds over time
3. View own integrity profile
4. Share with potential buyers

**Step 6: Finding Buyers**
1. Search for organic retailers
2. Filter by location and crop
3. View buyer profiles
4. Initiate contact
5. Negotiate terms

**Step 7: Selling & Contracting**
1. Agree on quantity and price
2. Create simple contract/agreement
3. Update production calendar
4. Deliver produce
5. Track payments

---

### Retailer Journey (End-to-End)

**Step 1: Onboarding**
1. Register as retailer/buyer
2. Complete business profile
3. Specify sourcing needs
4. Set location and radius

**Step 2: Farmer Discovery**
1. Search farmers by crop and location
2. Apply filters (organic stage, integrity score)
3. View farmer profiles
4. Review farm designs
5. Check production calendars

**Step 3: Verification**
1. Review integrity scores
2. Check organic journey timeline
3. Assess crop diversity
4. View reliability indicators

**Step 4: Sourcing**
1. Contact selected farmers
2. Discuss requirements
3. Negotiate terms
4. Create buying agreement

**Step 5: Ongoing Management**
1. Track deliveries
2. Record payments
3. Monitor supply consistency
4. Provide feedback (informal)
5. Renew or adjust contracts

---

## Data Models

### Farmer
```
farmer_id (PK, UUID)
mobile_number (VARCHAR, UNIQUE, NOT NULL)
name (VARCHAR, NOT NULL)
village (VARCHAR)
district (VARCHAR)
state (VARCHAR)
land_size_acres (DECIMAL)
water_source (ENUM: borewell, canal, rainfed)
irrigation_type (ENUM: drip, flood, none)
has_livestock (BOOLEAN)
farming_stage (ENUM: chemical, transition_year1, transition_year2, fully_organic)
family_labor_count (INTEGER)
monthly_expenses (DECIMAL)
registration_date (TIMESTAMP)
profile_status (ENUM: incomplete, complete)
last_updated (TIMESTAMP)
```

### Farm Design
```
design_id (PK, UUID)
farmer_id (FK -> Farmer)
total_area (DECIMAL)
buffer_zone_config (JSON)
  - width
  - trees: [name, spacing, purpose]
perennial_zone_config (JSON)
  - crops: [name, spacing, harvest_timeline, income_projection]
seasonal_zone_config (JSON)
  - crops: [name, cycle_days, rotation_plan]
visual_map_data (JSON)
  - coordinates
  - zone_boundaries
created_date (TIMESTAMP)
last_updated (TIMESTAMP)
```

### Crop
```
crop_id (PK, UUID)
crop_name (VARCHAR, NOT NULL)
crop_type (ENUM: perennial, seasonal, buffer)
region_suitability (JSON)
  - states: [state_name, suitability_score]
spacing_requirements (JSON)
  - row_spacing_ft
  - plant_spacing_ft
harvest_timeline_days (INTEGER)
income_potential (DECIMAL)
water_needs (ENUM: low, medium, high)
labor_intensity (ENUM: low, medium, high)
```

### Dry Period Analysis
```
analysis_id (PK, UUID)
farmer_id (FK -> Farmer)
analysis_date (TIMESTAMP)
risk_level (ENUM: low, medium, high)
dry_months (JSON ARRAY)
  - [month_number, income, expenses, gap]
gap_amount (DECIMAL)
survival_plan (JSON)
  - seasonal_crops: [crop_name, expected_income, planting_date]
```

### Cash Flow Entry
```
entry_id (PK, UUID)
farmer_id (FK -> Farmer)
entry_date (DATE)
entry_type (ENUM: income, expense)
crop_id (FK -> Crop, NULLABLE)
quantity (DECIMAL, NULLABLE)
price_per_unit (DECIMAL, NULLABLE)
total_amount (DECIMAL, NOT NULL)
notes (TEXT)
created_at (TIMESTAMP)
```

### Integrity Record
```
record_id (PK, UUID)
farmer_id (FK -> Farmer, UNIQUE)
chemical_exit_date (DATE)
days_chemical_free (INTEGER, COMPUTED)
crop_diversity_score (DECIMAL)
on_farm_inputs_usage (BOOLEAN)
integrity_score (DECIMAL, COMPUTED)
last_calculated (TIMESTAMP)
```

### Retailer
```
retailer_id (PK, UUID)
mobile_number (VARCHAR, UNIQUE, NOT NULL)
business_name (VARCHAR, NOT NULL)
business_type (ENUM: organic_store, exporter, housing_society, bulk_buyer)
location (VARCHAR)
latitude (DECIMAL)
longitude (DECIMAL)
service_radius_km (INTEGER)
crops_needed (JSON ARRAY)
  - [crop_name, quantity_range, frequency]
payment_terms (VARCHAR)
registration_date (TIMESTAMP)
profile_status (ENUM: incomplete, complete)
```

### Market Match
```
match_id (PK, UUID)
farmer_id (FK -> Farmer)
retailer_id (FK -> Retailer)
crop_id (FK -> Crop)
match_score (DECIMAL)
distance_km (DECIMAL)
status (ENUM: suggested, contacted, active, completed)
created_date (TIMESTAMP)
last_updated (TIMESTAMP)
```

### Contract
```
contract_id (PK, UUID)
farmer_id (FK -> Farmer)
retailer_id (FK -> Retailer)
crop_id (FK -> Crop)
quantity_agreed (DECIMAL)
price_per_unit (DECIMAL)
payment_terms (VARCHAR)
start_date (DATE)
end_date (DATE)
status (ENUM: active, completed, cancelled)
created_date (TIMESTAMP)
notes (TEXT)
```

### Production Calendar
```
calendar_id (PK, UUID)
farmer_id (FK -> Farmer)
crop_id (FK -> Crop)
planting_date (DATE)
expected_harvest_date (DATE)
estimated_quantity (DECIMAL)
actual_harvest_date (DATE, NULLABLE)
actual_quantity (DECIMAL, NULLABLE)
created_at (TIMESTAMP)
updated_at (TIMESTAMP)
```

---

## API Endpoints

### Authentication
```
POST   /api/auth/register
       Body: { user_type, mobile_number, name, password }
       Response: { user_id, token, user_type }

POST   /api/auth/login
       Body: { mobile_number, password }
       Response: { user_id, token, user_type, profile_status }

POST   /api/auth/send-otp
       Body: { mobile_number }
       Response: { success, message }

POST   /api/auth/verify-otp
       Body: { mobile_number, otp }
       Response: { verified, token }

POST   /api/auth/logout
       Headers: { Authorization: Bearer <token> }
       Response: { success }
```

### Farmer Profile
```
GET    /api/farmer/profile
       Headers: { Authorization: Bearer <token> }
       Response: { farmer_profile }

POST   /api/farmer/profile
       Headers: { Authorization: Bearer <token> }
       Body: { name, village, district, land_size, ... }
       Response: { farmer_id, profile_status }

PUT    /api/farmer/profile
       Headers: { Authorization: Bearer <token> }
       Body: { fields_to_update }
       Response: { updated_profile }

GET    /api/farmer/:id
       Response: { public_farmer_profile }
```

### Farm Design
```
POST   /api/farm/design/generate
       Headers: { Authorization: Bearer <token> }
       Body: { farmer_id, preferences }
       Response: { design_id, zones, visual_map }

GET    /api/farm/design/:farmerId
       Response: { farm_design }

PUT    /api/farm/design/:designId
       Headers: { Authorization: Bearer <token> }
       Body: { updated_zones }
       Response: { updated_design }

GET    /api/farm/design/:designId/visual
       Response: { visual_map_data }
```

### Risk & Dry Period
```
POST   /api/analysis/dry-period
       Headers: { Authorization: Bearer <token> }
       Body: { farmer_id, perennial_crops, seasonal_crops }
       Response: { analysis_id, risk_level, dry_months, survival_plan }

GET    /api/analysis/dry-period/:farmerId
       Response: { latest_analysis }

GET    /api/analysis/survival-plan/:farmerId
       Response: { survival_plan_details }
```

### Cash Flow
```
POST   /api/cashflow/entry
       Headers: { Authorization: Bearer <token> }
       Body: { entry_type, crop_id, quantity, price, total_amount }
       Response: { entry_id, running_balance }

GET    /api/cashflow/:farmerId
       Query: { start_date, end_date }
       Response: { entries[], summary }

GET    /api/cashflow/:farmerId/monthly/:month
       Response: { monthly_summary, income, expenses, balance }

GET    /api/cashflow/:farmerId/summary
       Response: { total_income, total_expenses, net_balance, trends }

DELETE /api/cashflow/entry/:entryId
       Headers: { Authorization: Bearer <token> }
       Response: { success }
```

### Integrity
```
GET    /api/integrity/:farmerId
       Response: { integrity_score, badges, metrics }

GET    /api/integrity/:farmerId/timeline
       Response: { organic_journey_timeline }

GET    /api/integrity/:farmerId/badges
       Response: { earned_badges[] }
```

### Retailer Profile
```
GET    /api/retailer/profile
       Headers: { Authorization: Bearer <token> }
       Response: { retailer_profile }

POST   /api/retailer/profile
       Headers: { Authorization: Bearer <token> }
       Body: { business_name, business_type, location, ... }
       Response: { retailer_id, profile_status }

PUT    /api/retailer/profile
       Headers: { Authorization: Bearer <token> }
       Body: { fields_to_update }
       Response: { updated_profile }
```

### Market Discovery
```
GET    /api/market/farmers
       Headers: { Authorization: Bearer <token> }
       Query: { location, radius, crop, organic_stage, min_integrity_score }
       Response: { farmers[], match_scores }

GET    /api/market/retailers
       Headers: { Authorization: Bearer <token> }
       Query: { location, radius, crop }
       Response: { retailers[], distances }

POST   /api/market/match
       Headers: { Authorization: Bearer <token> }
       Body: { farmer_id, retailer_id, crop_id }
       Response: { match_id, match_score }

GET    /api/market/matches/:userId
       Headers: { Authorization: Bearer <token> }
       Response: { matches[] }
```

### Contracts
```
POST   /api/contract
       Headers: { Authorization: Bearer <token> }
       Body: { farmer_id, retailer_id, crop_id, quantity, price, terms }
       Response: { contract_id }

GET    /api/contract/:contractId
       Headers: { Authorization: Bearer <token> }
       Response: { contract_details }

PUT    /api/contract/:contractId
       Headers: { Authorization: Bearer <token> }
       Body: { fields_to_update }
       Response: { updated_contract }

GET    /api/contract/farmer/:farmerId
       Headers: { Authorization: Bearer <token> }
       Response: { contracts[] }

GET    /api/contract/retailer/:retailerId
       Headers: { Authorization: Bearer <token> }
       Response: { contracts[] }
```

### Production Calendar
```
POST   /api/calendar/entry
       Headers: { Authorization: Bearer <token> }
       Body: { crop_id, planting_date, expected_harvest_date, quantity }
       Response: { calendar_id }

GET    /api/calendar/:farmerId
       Query: { start_date, end_date }
       Response: { calendar_entries[] }

PUT    /api/calendar/entry/:entryId
       Headers: { Authorization: Bearer <token> }
       Body: { fields_to_update }
       Response: { updated_entry }

DELETE /api/calendar/entry/:entryId
       Headers: { Authorization: Bearer <token> }
       Response: { success }
```

### Crops (Reference Data)
```
GET    /api/crops
       Query: { type, region }
       Response: { crops[] }

GET    /api/crops/:region
       Response: { region_specific_crops[] }

GET    /api/crops/:cropId
       Response: { crop_details }
```

---

## Business Logic

### Farm Design Generator Algorithm

**Inputs:**
- Land size
- Location (for regional crop selection)
- Water availability
- Farmer preferences

**Process:**
1. Calculate zone allocations:
   - Buffer Zone: 5-10% of perimeter
   - Perennial Zone: 40-50% of area
   - Seasonal Zone: 40-50% of area

2. Select buffer zone plants based on region

3. Select perennial crops:
   - Query crop database for region
   - Filter by water availability
   - Rank by income potential and farmer preference
   - Calculate spacing and tree count

4. Select seasonal crops:
   - Fast-growing vegetables
   - Rotation planning for continuous harvest
   - Income projection per cycle

5. Generate visual map coordinates

**Output:**
- 3-zone farm design
- Crop recommendations
- Spacing calculations
- Income timeline

---

### Dry Period Calculator Algorithm

**Inputs:**
- Perennial crop harvest timelines
- Seasonal crop cycles
- Monthly household expenses
- Current savings (optional)

**Process:**
1. Create 12-month projection array

2. For each month:
   - Calculate expected income from perennials
   - Calculate expected income from seasonals
   - Subtract monthly expenses
   - Identify deficit months

3. Calculate risk level:
   - Low: 0-2 deficit months
   - Medium: 3-5 deficit months
   - High: 6+ deficit months

4. Generate survival plan:
   - Identify gaps
   - Recommend fast-cash crops
   - Calculate planting schedule to fill gaps

**Output:**
- Month-by-month projection
- Risk level
- Dry months highlighted
- Survival plan with actionable steps

---

### Integrity Score Calculation

**Factors:**
1. Days since chemical exit (40% weight)
   - 0-180 days: 0-40 points
   - 181-365 days: 41-70 points
   - 365+ days: 71-100 points

2. Crop diversity (30% weight)
   - Number of different crops grown
   - Rotation consistency
   - Multilayer implementation

3. On-farm inputs (20% weight)
   - Livestock presence
   - Compost usage
   - No external chemical purchases

4. Production consistency (10% weight)
   - Regular cash-flow entries
   - Harvest tracking
   - Calendar maintenance

**Formula:**
```
Integrity Score = (Chemical_Free_Score * 0.4) + 
                  (Diversity_Score * 0.3) + 
                  (On_Farm_Score * 0.2) + 
                  (Consistency_Score * 0.1)
```

**Output:**
- Score: 0-100
- Badges earned
- Timeline visualization

---

### Market Matching Algorithm

**Inputs:**
- Retailer requirements (crop, location, quantity)
- Farmer profiles (location, crops, integrity, capacity)

**Process:**
1. Filter farmers by:
   - Crop availability
   - Location within radius
   - Minimum integrity threshold
   - Production capacity

2. Calculate match score for each farmer:
   - Distance proximity (30%)
   - Integrity score (30%)
   - Production capacity match (20%)
   - Historical reliability (20%)

3. Rank farmers by match score

4. Return top matches

**Output:**
- Ranked list of farmers
- Match scores
- Distance calculations
- Contact information

---

## Security Considerations

### Authentication
- JWT tokens with expiration
- Refresh token mechanism
- Secure password hashing (bcrypt, 10 rounds)
- OTP-based mobile verification

### Authorization
- Role-based access control (Farmer, Retailer)
- Resource ownership validation
- API endpoint protection

### Data Protection
- HTTPS encryption
- Input validation and sanitization
- SQL injection prevention (parameterized queries)
- XSS protection
- CSRF tokens for state-changing operations

### Privacy
- Profile visibility controls
- Contact information protection
- Data anonymization for analytics

---

## Performance Optimization

### Database
- Indexing on frequently queried fields:
  - mobile_number
  - farmer_id, retailer_id
  - location coordinates
  - dates
- Query optimization
- Connection pooling

### Caching
- Redis for session management
- Cache frequently accessed data:
  - Crop reference data
  - User profiles
  - Farm designs

### Frontend
- Code splitting
- Lazy loading of components
- Image optimization
- Minification and compression

### API
- Response pagination
- Rate limiting
- Gzip compression
- CDN for static assets

---

## Deployment Architecture

### Production Environment (AWS)

**Note:** This project is powered by AWS sponsorship, leveraging enterprise-grade cloud infrastructure.

```
                    ┌─────────────────────┐
                    │   Route 53 (DNS)    │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │  CloudFront (CDN)   │
                    │  + AWS WAF          │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │  Application Load   │
                    │     Balancer        │
                    └──────────┬──────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
┌───────▼────────┐    ┌───────▼────────┐    ┌───────▼────────┐
│  EC2 Instance  │    │  EC2 Instance  │    │  EC2 Instance  │
│  (App Server)  │    │  (App Server)  │    │  (App Server)  │
│  Auto Scaling  │    │  Auto Scaling  │    │  Auto Scaling  │
└───────┬────────┘    └───────┬────────┘    └───────┬────────┘
        │                      │                      │
        └──────────────────────┼──────────────────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
┌───────▼────────┐    ┌───────▼────────┐    ┌───────▼────────┐
│  RDS Primary   │◄───│  ElastiCache   │    │   S3 Bucket    │
│  (PostgreSQL)  │    │    (Redis)     │    │  (Files/Logs)  │
│    Multi-AZ    │    │                │    │                │
└───────┬────────┘    └────────────────┘    └────────────────┘
        │
┌───────▼────────┐
│  RDS Replica   │
│  (Read Only)   │
└────────────────┘
```

### AWS Infrastructure Components

**Networking Layer:**
- VPC with public and private subnets across 2+ Availability Zones
- Internet Gateway for public subnet
- NAT Gateway for private subnet outbound traffic
- Security Groups for fine-grained access control
- Network ACLs for subnet-level security

**Compute Layer:**
- EC2 Auto Scaling Group (2-8 instances based on load)
- Application Load Balancer with health checks
- Launch Template with user data for automated setup
- CloudWatch alarms for scaling triggers

**Database Layer:**
- RDS PostgreSQL Multi-AZ for high availability
- Read Replicas for read-heavy operations
- Automated backups with 7-day retention
- AWS Backup for additional backup management

**Caching Layer:**
- ElastiCache Redis cluster
- Session management
- Frequently accessed data caching

**Storage Layer:**
- S3 for user uploads, farm maps, documents
- S3 Lifecycle policies for cost optimization
- S3 Versioning for data protection
- CloudFront for global content delivery

**Security Layer:**
- AWS WAF for web application protection
- AWS Shield Standard (DDoS protection)
- AWS Certificate Manager for SSL/TLS
- AWS Secrets Manager for credentials
- IAM roles and policies
- Security Groups and NACLs
- VPC Flow Logs for network monitoring

**Monitoring & Logging:**
- CloudWatch for metrics and alarms
- CloudWatch Logs for application logs
- AWS X-Ray for distributed tracing
- CloudTrail for API audit logs
- SNS for alert notifications

**CI/CD Pipeline:**
- CodeCommit or GitHub for source control
- CodeBuild for building and testing
- CodeDeploy for automated deployment
- CodePipeline for orchestration
- ECR for Docker images (if containerized)

### Deployment Strategies

**Blue-Green Deployment:**
- Maintain two identical production environments
- Deploy to inactive environment (Green)
- Test thoroughly
- Switch traffic via Load Balancer
- Keep Blue environment for quick rollback
             OR
**Rolling Deployment:**
- Deploy to instances one at a time
- Maintain service availability
- Automatic rollback on health check failure
             OR
**Canary Deployment:**
- Deploy to small subset of instances
- Monitor metrics and errors
- Gradually increase traffic
- Full rollout or rollback based on results

### Disaster Recovery

**Backup Strategy:**
- RDS automated backups (daily)
- RDS snapshots (weekly)
- S3 versioning and replication
- Cross-region backup for critical data

**Recovery Objectives:**
- RTO (Recovery Time Objective): < 1 hour
- RPO (Recovery Point Objective): < 15 minutes

**Multi-Region Setup (Future):**
- Primary region: ap-south-1 (Mumbai)
- DR region: ap-southeast-1 (Singapore)
- Route 53 health checks and failover

### AWS Cost Optimization

**Implemented Strategies:**
- Reserved Instances for predictable workloads (up to 72% savings)
- Auto Scaling to match demand
- S3 Intelligent-Tiering for storage optimization
- CloudFront caching to reduce origin requests
- VPC Endpoints to avoid NAT Gateway costs
- Right-sizing based on CloudWatch metrics
- Spot Instances for non-critical workloads

---

## Conclusion

FarmFlow's design prioritizes simplicity, reliability, and ground-reality alignment. The architecture supports the core mission: helping organic multilayer farmers survive the transition period through systematic planning of cash-flow, labor, and direct selling. The dual-profile system creates a transparent marketplace where trust is built through verifiable integrity records, and both farmers and retailers benefit from reliable, poison-free supply chains.

**AWS Infrastructure Benefits:**
- Enterprise-grade reliability (99.99% uptime)
- Global scalability without infrastructure concerns
- Built-in security and compliance
- Cost-effective with sponsorship
- Comprehensive monitoring and disaster recovery

