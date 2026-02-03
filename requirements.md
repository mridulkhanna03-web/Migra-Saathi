# Requirements Document

## Introduction

MigraSaathi is a WhatsApp-based, voice-first relocation assistant designed to help internal migrants in India access essential services including PG accommodations, job opportunities, essential services, and guidance. The MVP focuses on Bangalore as a pilot city to enable execution within a hackathon timeline, leveraging AWS-powered AI tools to provide intelligent, conversational assistance.

## Glossary

- **MigraSaathi**: The WhatsApp-based relocation assistant system
- **User**: Internal migrants in India seeking relocation assistance
- **PG**: Paying Guest accommodation
- **POI**: Point of Interest (essential service locations like Aadhaar centers, ration shops)
- **Lex_Bot**: Amazon Lex chatbot interface component
- **Bedrock_Engine**: Amazon Bedrock AI service for Q&A responses
- **Location_Service**: Amazon Location Service for geographical queries
- **Data_Store**: DynamoDB database storing PGs, jobs, and POIs
- **Lambda_Handler**: AWS Lambda functions processing business logic
- **Comprehend_Service**: Amazon Comprehend for natural language processing

## Requirements

### Requirement 1: PG Accommodation Search

**User Story:** As an internal migrant, I want to search for PG accommodations based on my budget and location preferences, so that I can find suitable housing quickly.

#### Acceptance Criteria

1. WHEN a user sends a message like "PG under 6k near Whitefield", THE Lex_Bot SHALL extract budget and location parameters
2. WHEN budget and location are extracted, THE System SHALL query the Data_Store for matching PG listings
3. WHEN matching PGs are found, THE System SHALL return up to 3 PG listings with photos, contact details, and price
4. WHEN no matching PGs are found, THE System SHALL suggest alternative locations or budget ranges
5. WHEN PG search results are displayed, THE System SHALL format them clearly with all essential information

### Requirement 2: Job Lead Generation

**User Story:** As an internal migrant, I want to find job opportunities based on my skills and location, so that I can secure employment quickly.

#### Acceptance Criteria

1. WHEN a user requests job assistance, THE Lex_Bot SHALL ask for job role and location preferences
2. WHEN a user specifies "construction work near me", THE Comprehend_Service SHALL extract job type and location
3. WHEN job parameters are extracted, THE System SHALL query the Data_Store for matching job listings
4. WHEN matching jobs are found, THE System SHALL return up to 2 job cards with role, location, and contact information
5. WHEN no matching jobs are found, THE System SHALL suggest similar job types or nearby locations

### Requirement 3: Essential Services Location Finder

**User Story:** As an internal migrant, I want to find essential service locations like Aadhaar centers and ration shops, so that I can access government services easily.

#### Acceptance Criteria

1. WHEN a user asks "Where is Aadhaar office?", THE Comprehend_Service SHALL identify the service type requested
2. WHEN service type is identified, THE Location_Service SHALL find the nearest POI of that type
3. WHEN nearest POI is found, THE System SHALL return location details with address and directions
4. WHEN POI information is provided, THE System SHALL include basic how-to instructions for that service
5. WHEN no nearby POI is found, THE System SHALL suggest the next nearest location with distance information

### Requirement 4: City Information and Guidance

**User Story:** As an internal migrant, I want to get answers to common questions about city procedures and services, so that I can navigate bureaucratic processes effectively.

#### Acceptance Criteria

1. WHEN a user asks procedural questions like "How to update Aadhaar", THE Bedrock_Engine SHALL provide step-by-step guidance
2. WHEN city-specific information is requested, THE Bedrock_Engine SHALL provide Bangalore-specific context and procedures
3. WHEN guidance is provided, THE System SHALL format responses in clear, actionable steps
4. WHEN complex procedures are explained, THE System SHALL break them down into simple, sequential instructions
5. WHEN users ask follow-up questions, THE Bedrock_Engine SHALL maintain context and provide relevant additional information

### Requirement 5: Community Connection

**User Story:** As an internal migrant, I want to connect with other migrants from my region, so that I can build a support network and share experiences.

#### Acceptance Criteria

1. WHEN a user completes a service interaction, THE System SHALL offer community group recommendations
2. WHEN community connection is requested, THE System SHALL provide WhatsApp group links based on user's region
3. WHEN group recommendations are made, THE System SHALL provide brief descriptions of group purposes
4. WHEN users express interest in joining, THE System SHALL provide clear instructions for group participation
5. WHEN group links are shared, THE System SHALL include community guidelines and expectations

### Requirement 6: Natural Language Processing

**User Story:** As an internal migrant, I want to communicate in natural language without learning specific commands, so that I can interact with the system intuitively.

#### Acceptance Criteria

1. WHEN a user sends any message, THE Comprehend_Service SHALL analyze the text for intent and entities
2. WHEN budget amounts are mentioned, THE System SHALL extract numerical values and currency context
3. WHEN location names are mentioned, THE System SHALL identify and validate geographical references
4. WHEN job roles are mentioned, THE System SHALL categorize them into standard job types
5. WHEN ambiguous requests are received, THE System SHALL ask clarifying questions to better understand user needs

### Requirement 7: WhatsApp Integration

**User Story:** As an internal migrant, I want to access all services through WhatsApp, so that I can use a familiar platform without installing new applications.

#### Acceptance Criteria

1. WHEN a user sends a message to the WhatsApp number, THE Lex_Bot SHALL receive and process the message
2. WHEN responses are generated, THE System SHALL format them appropriately for WhatsApp display
3. WHEN images are included in responses, THE System SHALL ensure they display correctly in WhatsApp
4. WHEN conversations span multiple messages, THE System SHALL maintain session context
5. WHEN users restart conversations, THE System SHALL provide a helpful welcome message with available services

### Requirement 8: Data Management

**User Story:** As a system administrator, I want reliable data storage and retrieval for PGs, jobs, and POIs, so that users receive accurate and up-to-date information.

#### Acceptance Criteria

1. WHEN PG data is stored, THE Data_Store SHALL include all required fields: location, price, contact, photos
2. WHEN job data is stored, THE Data_Store SHALL include role, location, contact, and job type information
3. WHEN POI data is stored, THE Data_Store SHALL include service type, address, and operational details
4. WHEN data queries are executed, THE System SHALL return results within 2 seconds
5. WHEN data is retrieved, THE System SHALL ensure all required fields are present and valid