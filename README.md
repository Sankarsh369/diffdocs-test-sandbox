# diffdocs-test-sandbox

const mongoose = require('mongoose');

// Old Schema Setup
const UserSchema = new mongoose.Schema({
  username: { type: String, required: true },
  // ADDED: We are upgrading security by adding a role constraint
  role: { type: String, enum: ['user', 'admin'], default: 'user' },
  password: { type: String, required: true }
});

// ADDED: Middleware hook to catch errors before saving to MongoDB Atlas
UserSchema.post('save', function(error, doc, next) {
  if (error.name === 'MongoServerError' && error.code === 11000) {
    next(new Error('There was a duplicate key error in the cluster'));
  } else {
    next(error);
  }
});

module.exports = mongoose.model('User', UserSchema);
INFO:     Will watch for changes in these directories: ['C:\\Users\\DELL\\Desktop\\diffdocs-waitlist']
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [17448] using WatchFiles
INFO:     Started server process [27548]
INFO:     Waiting for application startup.
🚀 Booting DiffDocs Backend Services...
## 🚀 System Updates & Telemetry Checklist

- [x] Initialized MongoDB Atlas cloud production database storage cluster.
- [x] Verified high-performance asynchronous Google Gemini 1.5 core engine.
- [ ] Implement cryptographic HMAC-SHA256 GitHub signature validation hook.
- [ ] Deploy FastAPI application layers directly to a cloud provider environment.

### Architectural Note
All background pipelines are configured to communicate using non-blocking asynchronous event handling strategies to maximize server efficiency.



GEMINI_API_KEY=AIzaSy...your_actual_key...
