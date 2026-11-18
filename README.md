const joi = require('joi');

const userSchema = joi.object({
  email: joi.string().email().required(),
  password: joi.string().min(8).required()
});


// validate before processing
const { error, value } = userSchema.validate(req.body);


const bcrypt = require('bcrypt');


// hash password before storing
const saltrounds = 12;
const hashedpassword = await bcrypt.hash(password, saltrounds);

// verify password during login
const isValid = await bcrypt.compare(password, hashedpassword);


require('dotenv').config();

// Access environment variables
const dbUrl = process.env.DATABASE_URL;
const jwtsecret = process.env.JWT_SECRET;
const port = process.env.PORT || 3000;


// never Commit .env files to version control



// vulnerable to SQL injection
const query = `SELECT * FROM users WHERE id = ${userId}`;

// safe with parameterized queries
const query = `SELECT * FROM users WHERE id = ?`;
const result = await db.query(query, [userId]);

// or with named parameters
const result = await db.query(`SELECT * FROM users WHERE id = :id`, {id: userId});


const helmet = require('helmet');


// Apply security headers
app.use(helmet({
  contentSecurityPolicy: true,
  hsts: { maxAge: 31536000 },
  noSniff: true,
  xssFilter: true
}));


// Always use HTTPS in production



const rateLimit = require('express-rate-limit');


const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per windowMs
  message: 'Too many requests from this IP'
});


app.use(limiter);


# Check for vulnerabilities
npm audit

# Automatically fix issues
npm audit fix

# Force fix all vulnerabilities
npm audit fix --force

# use npm ci for production installs
npm ci



const logger = require('winston');

// Global error handler
app.use((err, req, res, next) => {
  logger.error(err.stack);

  // Don't leak stack traces in production
  const message = process.env.NODE_ENV === 'production'
    ? 'Internal Server Error' : err.message;

  res.status(500).json({ error: message });
});
