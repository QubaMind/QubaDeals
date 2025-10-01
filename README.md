# QubaDeals: AI-Powered Deals Aggregation Platform

## 1. Project Vision
QubaDeals is an AI-powered platform designed to aggregate, score, and deliver the best deals from across the web. Leveraging autonomous agents, machine learning, and scalable cloud infrastructure, QubaDeals provides users with high-quality, personalized deal recommendations in real time.

## 2. Agent-Based Architecture
QubaDeals is built on a modular, agent-based architecture. Each agent is responsible for a specific domain task and communicates via a message queue for robust, scalable orchestration.

### Agents Overview
- **Web Scraping Agent**: Collects deals from various e-commerce and coupon sites using headless browsers and APIs.
- **Data Processing Agent**: Normalizes, validates, and deduplicates raw deal data, ensuring consistency and quality.
- **ML Agent**: Scores deals using machine learning models based on relevance, price history, and user preferences.
- **Notification Agent**: Sends real-time alerts to users via email, SMS, or push notifications when high-quality deals are found.
- **API Gateway Agent**: Exposes RESTful endpoints for external integrations and partner platforms.

## 3. Folder Structure
```
/agents         # Individual agent modules (web_scraper, data_processor, ml, notification, api_gateway)
/shared         # Common utilities, data models, logging, error handling
/config         # Environment configs, secrets, agent settings
/tests          # Unit and integration tests for all agents and shared modules
/docs           # Technical documentation, architecture diagrams, API specs
README.md       # Project overview and setup instructions
```

## 4. Tech Stack
- **Language**: Python 3.10+
- **Web Framework**: FastAPI
- **Message Queue**: RabbitMQ
- **Cache**: Redis
- **Database**: PostgreSQL
- **Containerization**: Docker

## 5. Deployment
- **Orchestration**: Docker Compose for local and production deployments
- **Auto-Scaling**: Agents are stateless and can be horizontally scaled via Docker Compose or Kubernetes
- **Environment Management**: All configs managed via `/config` and `.env` files

## 6. Development Setup
### Prerequisites
- Python 3.10+
- Docker & Docker Compose
- RabbitMQ, Redis, PostgreSQL (can be run via Docker)

### Installation Steps
1. **Clone the repository:**
	```bash
	git clone https://github.com/QubaMind/QubaDeals.git
	cd QubaDeals
	```
2. **Copy environment variables:**
	```bash
	cp config/.env.example config/.env
	# Edit config/.env with your secrets and settings
	```
3. **Build and start services:**
	```bash
	docker-compose up --build
	```
4. **Run tests:**
	```bash
	docker-compose exec api_gateway pytest /tests
	```

## 7. Agent Communication
Agents communicate asynchronously via RabbitMQ message queues. Each agent subscribes to relevant topics and processes messages independently, enabling fault tolerance and scalability.

**Message Flow Example:**
1. Web Scraping Agent publishes raw deals to `deals.raw` queue.
2. Data Processing Agent consumes from `deals.raw`, normalizes, and publishes to `deals.processed`.
3. ML Agent consumes from `deals.processed`, scores, and publishes to `deals.scored`.
4. Notification Agent consumes from `deals.scored` and sends alerts.
5. API Gateway Agent exposes endpoints for external access and can trigger agent actions.

## 8. Getting Started Guide for Developers
1. **Set up your environment:**
	- Install Python, Docker, and Docker Compose
	- Configure environment variables in `/config/.env`
2. **Start all services:**
	- Use `docker-compose up --build` to launch all agents and dependencies
3. **Develop new agents:**
	- Create a new module in `/agents`
	- Implement agent logic using FastAPI and RabbitMQ client libraries
	- Add unit tests in `/tests`
4. **Run tests:**
	- Use `pytest` for Python modules
5. **Documentation:**
	- Add technical docs and API specs in `/docs`
6. **Contribute:**
	- Follow the contribution guidelines in `/docs/CONTRIBUTING.md`

---
For more details, see `/docs/architecture.md` and `/docs/api_spec.md`.