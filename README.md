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
