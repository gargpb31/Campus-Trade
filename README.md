# 🏪 Campus Trade - Student Marketplace Platform



## 🎯 Overview

**Campus Trade** is a modern, full-stack web application designed as a **peer-to-peer marketplace** for students. It enables students to buy, sell, and exchange items like books, electronics, accessories, and more within their campus community. The platform provides a secure, user-friendly interface with robust features for managing listings, user profiles, and transactions.

### 🌟 Key Highlights

- **Secure Student Network** - Only verified students can access the platform
- **Modern UI/UX** - Professional design with responsive layout
- **Real-time Features** - Dynamic content updates and notifications
- **Admin Dashboard** - Comprehensive management tools for administrators
- **File Upload System** - Image management for product listings

## ✨ Features

### 🔐 Authentication & Security

- **User Registration & Login** with email verification
- **Password Reset** via OTP email system
- **Session Management** with secure cookies
- **Role-based Access Control** (Student/Admin)

### 🛍️ Marketplace Features

- **Product Listings** with images, descriptions, and pricing
- **Advanced Search** with keyword filtering
- **Product Categories** for easy browsing
- **Contact Information** for buyer-seller communication
- **Product Management** (Create, Edit, Delete)

### 👤 User Profile Management

- **Personal Information** (Name, Contact, Room Number)
- **Profile Photo Upload** with preview functionality
- **Product History** - Track listed and sold items
- **Account Statistics** - View activity metrics

### 🎛️ Admin Features

- **User Management** - View and manage all registered users
- **Product Moderation** - Review and manage product listings
- **Platform Statistics** - Monitor user and product counts
- **Content Management** - Delete inappropriate content

### 📱 Responsive Design

- **Mobile-First Approach** - Optimized for all devices
- **Modern UI Components** - Cards, modals, notifications
- **Smooth Animations** - Enhanced user experience
- **Cross-Browser Compatibility** - Works on all modern browsers

## 🛠️ Technologies Used

### Frontend

- **HTML5** - Semantic markup
- **CSS3** - Modern styling with CSS Grid & Flexbox
- **JavaScript (ES6+)** - Dynamic functionality
- **EJS** - Server-side templating
- **Font Awesome** - Icon library

### Backend

- **Node.js** - Runtime environment
- **Express.js** - Web application framework
- **PostgreSQL** - Relational database
- **Multer** - File upload middleware
- **Nodemailer** - Email service integration
- **Express-session** - Session management

### Development Tools

- **Git** - Version control
- **npm** - Package management
- **Nodemon** - Development server (auto-restart)

## 📋 Prerequisites

Before running this application, make sure you have the following installed:

- **Node.js** (v14 or higher)
- **npm** (Node Package Manager)
- **PostgreSQL** (v12 or higher)
- **Git** (for cloning the repository)

### Installing Prerequisites

#### Node.js & npm

```bash
# Download from https://nodejs.org/
# Or use package manager
# macOS (using Homebrew)
brew install node

# Ubuntu/Debian
sudo apt update
sudo apt install nodejs npm
```

#### PostgreSQL

```bash
# macOS (using Homebrew)
brew install postgresql
brew services start postgresql

# Ubuntu/Debian
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/campus-trade.git
cd campus-trade
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Database Setup

#### Create Database

```bash
# Connect to PostgreSQL
psql -U postgres

# Create database
CREATE DATABASE campus_trade;

# Create user (optional)
CREATE USER campus_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE campus_trade TO campus_user;

# Exit PostgreSQL
\q
```

#### Initialize Database Schema

```bash
# Run the SQL queries from queries.sql
psql -U postgres -d campus_trade -f queries.sql
```

### 4. Environment Configuration

Create a `.env` file in the root directory:

```env
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=campus_trade
DB_USER=postgres
DB_PASSWORD=your_password

# Server Configuration
PORT=3000
NODE_ENV=development

# Email Configuration (for OTP)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password

# Session Secret
SESSION_SECRET=your_session_secret_key
```

### 5. Update Database Connection

Edit the database connection in `solution.js`:

```javascript
const db = new Client({
  host: process.env.DB_HOST || "localhost",
  port: process.env.DB_PORT || 5432,
  database: process.env.DB_NAME || "campus_trade",
  user: process.env.DB_USER || "postgres",
  password: process.env.DB_PASSWORD || "your_password",
});
```

## ▶️ How to Run

### Development Mode

```bash
# Start the development server
npm run dev

# Or start directly
node solution.js
```

### Production Mode

```bash
# Install production dependencies
npm install --production

# Start the server
npm start
```

### Access the Application

- **Local Development**: http://localhost:3000
- **Network Access**: http://your-ip-address:3000

## 📁 Project Structure

```
Campus-Trade/
├── css/
│   └── styles.css              # Main CSS file
├── public/
│   ├── css/                    # Static CSS files
│   ├── uploads/                # User uploaded images
│   └── *.jpg                   # Static images
├── views/
│   ├── partials/               # Reusable EJS components
│   ├── *.ejs                   # Page templates
│   └── styles.css              # Page-specific styles
├── solution.js                 # Main server file
├── package.json                # Dependencies and scripts
├── queries.sql                 # Database schema
└── README.md                   # Project documentation
```

## 🔌 API Endpoints

### Authentication

- `POST /register` - User registration
- `POST /login` - User login
- `POST /send-otp` - Send password reset OTP
- `POST /verify-otp` - Verify OTP
- `POST /reset-password` - Reset password

### Products

- `GET /pro` - Get all products
- `POST /create` - Create new product
- `GET /edit/:id` - Edit product form
- `POST /edit/:id` - Update product
- `POST /delete/:id` - Delete product
- `GET /search` - Search products

### User Management

- `GET /up` - User profile
- `GET /edit-profile` - Edit profile form
- `POST /update-profile` - Update profile
- `GET /api/user-products` - Get user's products
- `GET /api/user-stats` - Get user statistics

### Admin (Protected)

- `GET /admin/products` - Admin products dashboard
- `POST /admin/delete-product/:id` - Delete product (admin)
- `GET /admin/users` - Admin users dashboard
- `POST /admin/delete-user/:id` - Delete user (admin)

## 🗄️ Database Schema

### Users Table

```sql
CREATE TABLE userinfo (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    name VARCHAR(255),
    enroll_no VARCHAR(50),
    contact VARCHAR(20),
    room_no VARCHAR(20),
    profile_photo VARCHAR(255),
    role VARCHAR(20) DEFAULT 'student',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Posts Table

```sql
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    image_url VARCHAR(255),
    expected_amount DECIMAL(10,2) NOT NULL,
    mobile_number VARCHAR(20),
    email_address VARCHAR(255),
    user_email VARCHAR(255) REFERENCES userinfo(email),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines

- Follow the existing code style
- Add comments for complex logic
- Test your changes thoroughly
- Update documentation if needed

## 🔮 Future Enhancements

### Planned Features

- 🔹 **Real-time Chat System** - Direct messaging between buyers and sellers
- 🔹 **Payment Gateway Integration** - Secure online transactions
- 🔹 **AI Price Suggestions** - Machine learning-based pricing recommendations
- 🔹 **Push Notifications** - Real-time updates for new listings
- 🔹 **Advanced Search Filters** - Category, price range, location-based search
- 🔹 **Review & Rating System** - User feedback and reputation management
- 🔹 **Mobile App** - Native iOS and Android applications
- 🔹 **Analytics Dashboard** - Detailed platform usage statistics

### Technical Improvements

- 🔹 **API Documentation** - Swagger/OpenAPI specification
- 🔹 **Unit Testing** - Jest test suite
- 🔹 **Docker Support** - Containerized deployment
- 🔹 **CI/CD Pipeline** - Automated testing and deployment
- 🔹 **Performance Optimization** - Caching and database optimization

## 📞 Support

If you encounter any issues or have questions:

- **Email**: support@campustrade.com
- **Issues**: [GitHub Issues](https://github.com/yourusername/campus-trade/issues)
- **Documentation**: Check this README and inline code comments

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Developer

**Sunny Garg** - Competitive Programmer & Full-Stack Developer

- **Portfolio**: [https://portfolio-sunny-gargs-projects.vercel.app/](https://portfolio-sunny-gargs-projects.vercel.app/)
- **LinkedIn**: [https://www.linkedin.com/in/gargpb31/](https://www.linkedin.com/in/gargpb31/)
- **GitHub**: [@gargpb31](https://github.com/gargpb31)

---

⭐ **Star this repository if you find it helpful!**

⚡ **Fun Fact**: The most expensive item ever sold online was a **$168 million yacht** auctioned through eBay! 🚢💰
