### ExpressJS Cheatsheet

------

- **Authorization middleware**

  use code below to do authorization on express JS

  ```javascript
  const jwt = require('jsonwebtoken');
  
  module.exports = (req, res, next) => {
    const token = req.header('auth-token');
    if (!token) return res.status(401).send({ message: 'Access Denied' });
  
    try {
      const verified = jwt.verify(token, process.env.TOKEN_SECRET);
      req.user = verified;
      return next();
    } catch (err) {
      res.status(400).send({ message: 'Invalid Token' });
    }
  };
  ```