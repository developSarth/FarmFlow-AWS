# Requirements Document: FarmFlow App

## Project Overview

FarmFlow is a web-based application designed to help organic multilayer farmers survive and thrive through systematic planning of cash-flow, labor, and direct selling. Unlike advisory apps, FarmFlow is a planning + survival + selling system that addresses the ground reality: organic multilayer farming is profitable only when diversification, cost control, and right buyer discovery are planned month-by-month.

### AWS Sponsorship

**This project is powered by AWS (Amazon Web Services) sponsorship**, providing access to enterprise-grade cloud infrastructure and services. This sponsorship enables:

- Reduced infrastructure costs (estimated 60-70% savings)
- Access to premium AWS services (RDS Multi-AZ, ElastiCache, CloudFront, etc.)
- Enhanced security features (WAF, Shield, GuardDuty)
- Scalability without significant cost increases
- AWS technical support and architecture guidance
- Free tier benefits for first 12 months
- Credits for compute, storage, and data transfer

**Key Benefits:**
- Year 1 infrastructure savings: $10,000-15,000
- Ongoing annual savings: $8,000-12,000
- Enterprise-grade reliability and security
- Global CDN for fast content delivery
- Automated backups and disaster recovery
- Compliance certifications (ISO, SOC, HIPAA-ready)

---

## Core Requirements

## Technology Stack

### Frontend

**Framework & Libraries:**
- React.js 18+ (UI framework)
- React Router (navigation)
- Redux Toolkit or Context API (state management)
- Axios (HTTP client)
- React Hook Form (form handling)
- Chart.js or Recharts (data visualization)
- Leaflet or Google Maps API (map visualization)
- i18next (internationalization)
- Tailwind CSS or Material-UI (styling)

**Build Tools:**
- Vite or Create React App
- ESLint (linting)
- Prettier (code formatting)

**Estimated Cost:**
- Development: Open source (free)
- CDN: $20-50/month (Cloudflare or AWS CloudFront)

---

### Backend

**Framework:**
- Node.js 18+ with Express.js
- OR Python 3.10+ with FastAPI/Django

**Libraries & Tools:**
- JWT (jsonwebtoken) - authentication
- Bcrypt - password hashing
- Joi or Yup - input validation
- Winston or Pino - logging
- Node-cron - scheduled tasks
- Nodemailer - email
- Twilio or MSG91 - SMS/OTP

**Estimated Cost:**
- Development: Open source (free)
- SMS/OTP service: $50-200/month (depending on volume)
- Email service: $10-50/month (SendGrid, AWS SES)

---

### Database

**Primary Database:**
- PostgreSQL 14+ (recommended)
- OR MySQL 8+

**Caching:**
- Redis 7+ (session management, caching)

**Estimated Cost:**
- Development: Free (local/Docker)
- Production: $50-200/month (managed service)
- Redis: $20-100/month

---

### Infrastructure & Hosting

**Cloud Provider: AWS (Amazon Web Services)**

*Note: This project is powered by AWS sponsorship, leveraging their comprehensive cloud infrastructure and services.*

**AWS Services Stack:**

**Compute:**
- EC2 instances (app servers) - t3.medium or t3.large
- Auto Scaling Groups for dynamic scaling
- Elastic Load Balancer (Application Load Balancer)
- AWS Lambda (serverless functions for background tasks)

**Database:**
- RDS PostgreSQL (Multi-AZ for high availability)
- RDS Read Replicas for read-heavy operations
- ElastiCache for Redis (caching and sessions)
- AWS Backup (automated backup management)

**Storage:**
- S3 (file storage for images, documents, backups)
- S3 Glacier (long-term backup archival)
- S3 Intelligent-Tiering (cost optimization)

**Content Delivery:**
- CloudFront (CDN for global content delivery)
- Route 53 (DNS management)

**Networking:**
- VPC (Virtual Private Cloud) for network isolation
- Security Groups and NACLs
- NAT Gateway for private subnet internet access
- VPC Peering (if multi-region)

**Monitoring & Management:**
- CloudWatch (monitoring, logging, alarms)
- CloudWatch Logs for centralized logging
- AWS X-Ray (distributed tracing)
- AWS Systems Manager (infrastructure management)
- AWS CloudTrail (audit logging)

**Security:**
- AWS WAF (Web Application Firewall)
- AWS Shield (DDoS protection)
- AWS Certificate Manager (SSL/TLS certificates - free)
- AWS Secrets Manager (API keys, credentials)
- IAM (Identity and Access Management)
- AWS GuardDuty (threat detection)

**CI/CD:**
- AWS CodePipeline (continuous delivery)
- AWS CodeBuild (build automation)
- AWS CodeDeploy (deployment automation)
- ECR (Elastic Container Registry) for Docker images

**Communication Services:**
- AWS SNS (SMS/push notifications)
- AWS SES (email service)
- AWS Pinpoint (user engagement)

**Additional Services:**
- AWS EventBridge (scheduled tasks, event-driven architecture)
- AWS Step Functions (workflow orchestration)
- AWS Amplify (optional for frontend hosting)
- AWS API Gateway (optional for API management)

---

### DevOps & Monitoring

**AWS-Native Tools:**
- AWS CodePipeline + CodeBuild + CodeDeploy (CI/CD)
- AWS CloudWatch (monitoring, alarms, dashboards)
- AWS X-Ray (application performance monitoring)
- AWS CloudTrail (audit and compliance)
- AWS Config (resource configuration tracking)
- Docker + ECR (containerization)
- Nginx (reverse proxy on EC2)
- PM2 (process management for Node.js)

**Third-Party Integration (Optional):**
- Sentry (error tracking) - $26-80/month
- GitHub Actions (alternative CI/CD) - free tier available

**Estimated Cost:**
- CI/CD (AWS native): Included in AWS sponsorship
- Monitoring (CloudWatch): $10-50/month (beyond free tier)
- Error tracking (Sentry): $26-80/month (optional)

---

### Third-Party Services

**Required:**
- SMS/OTP: AWS SNS (included in AWS sponsorship) or MSG91 for India-specific ($50-200/month)
- Maps API: Google Maps or Mapbox ($0-200/month based on usage)
- Email: AWS SES (included in AWS sponsorship, very cost-effective)

**Optional:**
- Payment Gateway: Razorpay, Stripe (2-3% transaction fee)
- Push Notifications: AWS SNS or Firebase Cloud Messaging (free)
- Analytics: AWS CloudWatch Insights (included) or Google Analytics (free)

**Note:** With AWS sponsorship, SNS and SES costs are significantly reduced or covered.


### 1. Farmer Profile Management

**Must Have:**
- Mobile number-based registration and authentication
- Reality-based input forms (land size, water source, irrigation, livestock, farming stage, labor, expenses)
- Profile editing capability
- Local language support (minimum: Hindi, English)
- Mobile-responsive interface

**Should Have:**
- Profile completion progress indicator
- Photo upload for farmer profile
- Location auto-detection via GPS

**Nice to Have:**
- Voice input for data entry
- Profile verification badges

---

### 2. Organic Farm Blueprint Generator

**Must Have:**
- 3-zone farm design generation (Buffer, Perennial, Seasonal)
- Region-specific crop recommendations
- Spacing calculations and tree/plant counts
- Simple visual farm map
- Zone-wise explanations in local language
- Downloadable/printable design

**Should Have:**
- Interactive map editing
- Multiple design variations
- Crop substitution suggestions
- Year-wise income timeline visualization

**Nice to Have:**
- 3D farm visualization
- AR-based farm layout preview
- Soil test integration

---

### 3. Transition Risk & Dry Period Calculator

**Must Have:**
- 12-month income vs expense projection
- Dry period identification (months where income < expenses)
- Risk level calculation (Low/Medium/High)
- Seasonal survival plan with crop recommendations
- Visual timeline with color-coded warnings

**Should Have:**
- Multiple scenario planning
- Savings integration
- Gap amount calculations
- Export to PDF

**Nice to Have:**
- What-if analysis tool
- Loan requirement calculator
- Government scheme suggestions

---

### 4. Monthly Cash-Flow Tracker

**Must Have:**
- Simple income/expense entry (crop, quantity, price)
- Monthly summary view
- Running balance calculation
- Visual indicators (Safe/Unsafe months)
- Trend analysis
- Actionable suggestions

**Should Have:**
- Offline data entry with sync
- Bulk entry capability
- Category-wise expense tracking
- Export to Excel/CSV

**Nice to Have:**
- Receipt photo upload
- Voice-based entry
- Automated SMS parsing for sales

---

### 5. Organic Integrity Record

**Must Have:**
- Automatic tracking of organic practices
- Days since chemical exit calculation
- Crop diversity scoring
- Integrity score (0-100)
- Visual timeline of organic journey
- Retailer-visible profile

**Should Have:**
- Verifiable badges (1 Year Chemical-Free, Diverse Cropping, etc.)
- Farm visit logs
- Third-party verification integration

**Nice to Have:**
- Blockchain-based verification
- QR code for instant verification
- Video testimonials

---

### 6. Retailer Profile Management

**Must Have:**
- Business registration and authentication
- Business type selection (organic store, exporter, bulk buyer, etc.)
- Location and service radius
- Crop requirements specification
- Payment terms definition

**Should Have:**
- Business verification (document upload)
- Multiple location support
- Sourcing calendar

**Nice to Have:**
- Certification management
- Buyer ratings and reviews

---

### 7. Market Discovery & Matching

**Must Have:**
- Farmer search by location, crop, organic stage
- Retailer search by location and crop needs
- Distance calculation
- Match score algorithm
- Direct contact capability
- Filter and sort options

**Should Have:**
- Map-based search interface
- Match suggestions/recommendations
- Saved searches
- Contact history

**Nice to Have:**
- AI-powered matching
- Predictive supply-demand analysis
- Automated match notifications

---

### 8. Contracts & Payment Management

**Must Have:**
- Simple contract creation (crop, quantity, price, terms)
- Contract status tracking
- Payment recording
- Delivery scheduling
- Contract history

**Should Have:**
- Contract templates
- Payment reminders
- Dispute notes
- SMS/email notifications

**Nice to Have:**
- Digital signatures
- Escrow payment integration
- Automated invoicing

---

### 9. Production Calendar

**Must Have:**
- Planting date entry
- Expected harvest date
- Estimated quantity
- Calendar view (month-wise)
- Retailer-visible schedule

**Should Have:**
- Harvest reminders
- Bulk entry
- Actual vs estimated tracking
- Export capability

**Nice to Have:**
- Weather-based adjustments
- Automated harvest predictions
- Integration with farm design

---

### 10. Authentication & Security

**Must Have:**
- Mobile OTP-based authentication
- Password-based login
- JWT token management
- Role-based access control (Farmer, Retailer)
- Secure password storage
- HTTPS encryption

**Should Have:**
- Two-factor authentication
- Session management
- Password recovery
- Account deactivation

**Nice to Have:**
- Biometric authentication
- Single sign-on (SSO)

---

## Non-Functional Requirements

### Performance
- Page load time: < 3 seconds on 3G connection
- API response time: < 500ms for 95% of requests
- Support: 10,000+ concurrent users
- Database query optimization with indexing

### Security
- HTTPS encryption for all communications
- Secure password hashing (bcrypt, 10+ rounds)
- Input validation and sanitization
- SQL injection prevention
- XSS protection
- Rate limiting on API endpoints
- Regular security audits

### Usability
- Mobile-first responsive design
- Local language support (Hindi, Tamil, Telugu, Kannada, Marathi)
- Simple, non-technical language
- Maximum 3 clicks to complete any task
- Offline capability for data entry
- Accessibility compliance (WCAG 2.1 Level AA)

### Reliability
- 99.5% uptime SLA
- Automated daily backups
- Disaster recovery plan
- Error logging and monitoring
- Graceful error handling
- Data validation at multiple layers

### Scalability
- Horizontal scaling capability
- Database replication
- Caching strategy (Redis)
- CDN for static assets
- Load balancing
- Support for 100,000+ users

### Maintainability
- Clean code architecture
- Comprehensive documentation
- Unit test coverage: > 80%
- Integration tests for critical flows
- Version control (Git)
- CI/CD pipeline

---

## Production Cost Estimates

### Phase 1: MVP Development (3-4 months)

**Development Team:**
- 1 Full-stack Developer: $4,000-6,000/month × 4 = $16,000-24,000
- 1 UI/UX Designer: $3,000-5,000/month × 2 = $6,000-10,000
- 1 QA Engineer: $2,500-4,000/month × 2 = $5,000-8,000
- 1 Project Manager (part-time): $2,000-3,000/month × 4 = $8,000-12,000

**Total Development Cost: $35,000-54,000**

**Alternative (Outsourcing to India):**
- Development Team: $15,000-25,000 (significantly lower)

---

### Infrastructure Costs (Monthly) - AWS-Based

**Note:** With AWS sponsorship, infrastructure costs are significantly reduced. The following estimates assume partial sponsorship coverage with some out-of-pocket expenses.

**Small Scale (0-1,000 users):**
- EC2 instances (2× t3.medium): $60-70
- RDS PostgreSQL (db.t3.medium): $70-90
- ElastiCache Redis (cache.t3.micro): $15-20
- S3 Storage: $5-10
- CloudFront CDN: $10-20
- Application Load Balancer: $20-25
- CloudWatch (beyond free tier): $10-20
- Route 53: $5
- SMS/OTP (MSG91 for India): $50-100
- Domain: $10-15

**Total: $255-375/month**
**With AWS Sponsorship: $50-150/month** (estimated out-of-pocket)

---

**Medium Scale (1,000-10,000 users):**
- EC2 instances (4× t3.large): $240-280
- RDS PostgreSQL (db.r5.large, Multi-AZ): $300-350
- ElastiCache Redis (cache.t3.small): $30-40
- S3 Storage: $20-40
- CloudFront CDN: $50-80
- Application Load Balancer: $25-30
- CloudWatch: $30-50
- NAT Gateway: $45-60
- AWS Backup: $20-30
- SMS/OTP: $200-500
- AWS WAF: $20-30

**Total: $980-1,490/month**
**With AWS Sponsorship: $300-600/month** (estimated out-of-pocket)

---

**Large Scale (10,000-100,000 users):**
- EC2 instances (8× t3.xlarge + Auto Scaling): $900-1,100
- RDS PostgreSQL (db.r5.xlarge, Multi-AZ + Read Replicas): $800-1,000
- ElastiCache Redis (cache.r5.large cluster): $300-400
- S3 Storage: $100-150
- CloudFront CDN: $200-300
- Application Load Balancer: $40-50
- CloudWatch + X-Ray: $100-150
- NAT Gateway: $90-120
- AWS Backup: $50-80
- AWS WAF + Shield: $50-80
- SMS/OTP: $1,000-2,000
- Secrets Manager: $10-20

**Total: $3,640-5,450/month**
**With AWS Sponsorship: $1,500-2,500/month** (estimated out-of-pocket)

---

### Annual Cost Summary (With AWS Sponsorship)

**Year 1 (Development + Operations):**
- Development: $35,000-54,000 (one-time)
- Infrastructure (avg 6 months small, 6 months medium): $1,800-4,500
- Third-party services (SMS, Maps): $3,000-6,000
- Contingency (15%): $5,820-9,675
- **Total Year 1: $45,620-74,175**

**Year 2+ (Operations only):**
- Infrastructure (medium scale with AWS sponsorship): $3,600-7,200/year
- Third-party services: $6,000-12,000/year
- Maintenance & Updates: $10,000-20,000/year
- Support & Bug Fixes: $5,000-10,000/year
- **Total Year 2+: $24,600-49,200/year**

**Savings from AWS Sponsorship:**
- Year 1: $10,000-15,000 saved
- Year 2+: $8,000-12,000/year saved

---

### Cost Optimization Strategies (AWS-Specific)

1. **AWS Reserved Instances** for predictable workloads (up to 72% savings)
2. **AWS Savings Plans** for flexible compute usage (up to 66% savings)
3. **Spot Instances** for non-critical workloads (up to 90% savings)
4. **S3 Intelligent-Tiering** for automatic storage cost optimization
5. **AWS Lambda** for serverless background tasks (pay per execution)
6. **CloudFront caching** to reduce origin requests and data transfer
7. **RDS Reserved Instances** for database (up to 69% savings)
8. **Auto Scaling** to match demand and avoid over-provisioning
9. **AWS Cost Explorer** and **AWS Budgets** for cost monitoring
10. **Right-sizing** EC2 instances based on CloudWatch metrics
11. **S3 Lifecycle policies** to move old data to Glacier
12. **VPC Endpoints** to avoid NAT Gateway costs for AWS services
13. **AWS Free Tier** maximization for first 12 months

**Optimized Costs with AWS Best Practices:**
- Year 1: $35,000-50,000 (with aggressive optimization)
- Year 2+: $18,000-35,000/year

---

## AWS Deployment Architecture

### Production Environment (AWS)

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

### Deployment Strategy

**Blue-Green Deployment:**
- Maintain two identical production environments
- Deploy to inactive environment (Green)
- Test thoroughly
- Switch traffic via Load Balancer
- Keep Blue environment for quick rollback

**Rolling Deployment:**
- Deploy to instances one at a time
- Maintain service availability
- Automatic rollback on health check failure

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

---

## Development Phases & Timeline

### Phase 1: MVP (3-4 months)
**Features:**
- Farmer profile and onboarding
- Basic farm design generator (3 zones)
- Dry period calculator
- Simple cash-flow tracker
- Retailer profile
- Basic market discovery
- Authentication

**Deliverables:**
- Web application (responsive)
- Admin panel (basic)
- API documentation
- User documentation

---

### Phase 2: Enhanced Features (2-3 months)
**Features:**
- Visual farm maps
- Integrity score system
- Production calendar
- Contract management
- Advanced market matching
- Multi-language support (5 languages)
- Offline capability

**Deliverables:**
- Enhanced web application
- Mobile PWA
- Analytics dashboard

---

### Phase 3: Scale & Optimize (2-3 months)
**Features:**
- Performance optimization
- Regional expansion
- Payment integration
- Advanced analytics
- Mobile app (React Native)
- Community features

**Deliverables:**
- Native mobile apps (iOS, Android)
- Advanced admin dashboard
- API v2 with improvements

---

## Success Metrics & KPIs

### User Adoption
- Target: 1,000 farmers in Year 1
- Target: 100 retailers in Year 1
- Profile completion rate: > 80%
- Monthly active users: > 60%

### Engagement
- Average session duration: > 5 minutes
- Cash-flow entries per farmer: > 4/month
- Farmer-retailer connections: > 500 in Year 1

### Business Impact
- Farmer income stability improvement: > 20%
- Contract completion rate: > 75%
- Average time to first sale: < 30 days
- User retention (6 months): > 50%

---

## Risks & Mitigation

### Technical Risks
- **Risk:** Poor internet connectivity in rural areas
  - **Mitigation:** Offline-first architecture, data sync
  
- **Risk:** Low digital literacy
  - **Mitigation:** Simple UI, voice input, video tutorials

- **Risk:** Scalability issues
  - **Mitigation:** Cloud-native architecture, auto-scaling

### Business Risks
- **Risk:** Low farmer adoption
  - **Mitigation:** Partnerships with NGOs, government schemes
  
- **Risk:** Retailer trust issues
  - **Mitigation:** Integrity score system, verification process

- **Risk:** Competition from existing platforms
  - **Mitigation:** Focus on organic niche, unique dry period calculator

---

## Compliance & Legal

### Data Privacy
- GDPR compliance (if serving EU users)
- India's Personal Data Protection Act compliance
- Privacy policy and terms of service
- User consent management
- Data encryption at rest and in transit

### Agricultural Regulations
- Compliance with organic certification standards
- No false claims about organic status
- Transparent integrity scoring methodology

### Financial
- If payment integration: PCI DSS compliance
- Tax compliance for transactions
- Proper invoicing and record-keeping

---

## Support & Maintenance

### Support Channels
- In-app help and FAQs
- WhatsApp support (cost-effective for India)
- Email support
- Phone support (limited hours)
- Video tutorials

### Maintenance
- Regular security updates
- Bug fixes (within 48 hours for critical)
- Feature updates (quarterly)
- Database maintenance and optimization
- Backup verification (weekly)

**Estimated Cost:**
- Support team (2 people): $3,000-5,000/month
- Maintenance developer: $2,000-4,000/month
- **Total: $5,000-9,000/month**

---

## Conclusion

FarmFlow addresses a critical gap in the organic farming ecosystem by focusing on survival planning rather than just advisory. With AWS sponsorship, the estimated investment of $35,000-54,000 for MVP development and $50-150/month for initial infrastructure (significantly reduced from standard costs) makes it a highly viable project with clear ROI potential through subscription models, commission on contracts, or government/NGO partnerships.

**AWS Infrastructure Advantages:**
- Enterprise-grade reliability (99.99% uptime SLA)
- Global scalability without infrastructure concerns
- Built-in security and compliance features
- Cost-effective scaling from 100 to 100,000+ users
- Comprehensive monitoring and analytics
- Disaster recovery and automated backups

The technology stack is modern, scalable, and leverages AWS-native services for optimal performance and cost-efficiency. The phased approach allows for iterative development and validation of assumptions before scaling.

**Key Differentiators:**
- Honest, ground-reality approach
- Dry period calculator (unique feature)
- Integrity score system
- Dual-profile marketplace
- Focus on cash-flow survival
- AWS-powered reliability and scalability

