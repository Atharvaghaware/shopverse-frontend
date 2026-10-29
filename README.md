# ShopVerse — Full-stack e-commerce starter

A responsive Amazon-inspired e-commerce starter using React + Vite, Java 21 + Spring Boot, PostgreSQL, and Docker/Render deployment configuration.

## Included
- Responsive storefront with search, category filters, product cards, cart, quantity controls, checkout form, and order tracking timeline
- React frontend with API fallback to demo products if backend is not configured
- Spring Boot REST API with product listing/search, product details, order creation, order lookup/tracking, health endpoint
- PostgreSQL persistence through Spring Data JPA
- Dockerfiles and `render.yaml` deployment blueprint

## Important scope note
This is a deployable MVP foundation, not a production-equivalent Amazon clone. Real payment processing, email/SMS, courier GPS, returns/refunds, seller marketplace, reviews moderation, advanced recommendations, and production-grade authentication require provider credentials and additional implementation. The checkout currently creates a demo order and does **not** charge a card. Do not collect real payment credentials in this demo.

## Run locally
Requirements: Java 21+, Node.js 20+, npm, PostgreSQL (or Docker).

### Backend
```bash
cd backend
# Set DATABASE_URL, DB_USERNAME, DB_PASSWORD if not using local defaults
mvn spring-boot:run
```
Default local database URL: `jdbc:postgresql://localhost:5432/shopverse`
API base URL: `http://localhost:8080/api`
Health: `http://localhost:8080/actuator/health`

### Frontend
```bash
cd frontend
cp .env.example .env
npm install
npm run dev
```
Open the URL printed by Vite. Set `VITE_API_BASE_URL=http://localhost:8080/api` in `.env`.

## Render deployment
1. Push this project to a GitHub repository.
2. In Render, create a new Blueprint and select the repository containing `render.yaml`.
3. Render will create a PostgreSQL database, backend web service, and static frontend site.
4. Set `VITE_API_BASE_URL` on the frontend to the backend URL plus `/api`. The blueprint includes a placeholder; update it to your actual backend URL if needed, then redeploy frontend.
5. For a production launch, configure a real domain, CORS origin, secrets, payment provider, and email/SMS provider.

## API
- `GET /api/products?q=&category=`
- `GET /api/products/{id}`
- `POST /api/orders`
- `GET /api/orders/{id}`
- `GET /api/orders/{id}/tracking`
- `GET /api/health`

## Production checklist
- Add secure user authentication, email verification, password reset, and role-based admin access.
- Integrate Razorpay/Stripe in test mode and verify payment status server-side.
- Integrate a courier/shipping provider for genuine shipment events and GPS only when the carrier supports it.
- Add rate limiting, request validation, audit logs, backups, monitoring, privacy policy, terms, returns policy, and security testing.

## Static UI phase
Added static design previews for an admin dashboard, seller centre, product catalogue editing, wishlist, review UI, and privacy/terms/shipping/accessibility/security checklists. These previews use sample data and browser-local state; they are not secured or persisted to PostgreSQL. Implement authenticated APIs and authorization before production use.
"# shopverse-frontend" 
