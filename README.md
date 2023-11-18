# profile
this project is based node.js
const express = require('express');
const app = express();
const port = 3000;

const users = [
 { id: 1, name: 'John Doe', age: 28, email: 'john@example.com' },
 { id: 2, name: 'Jane Doe', age: 25, email: 'jane@example.com' },
];

app.use(express.json());


app.get('/profile/:id', (req, res) => {
 const user = users.find(u => u.id === parseInt(req.params.id));
 if (!user) return res.status(404).send('User not found');
 res.send(user);
});


app.put('/profile/:id', (req, res) => {
 const user = users.find(u => u.id === parseInt(req.params.id));
 if (!user) return res.status(404).send('User not found');


 user.name = req.body.name;
 user.age = req.body.age;
 user.email = req.body.email;

 res.send(user);
});


app.delete('/profile/:id', (req, res) => {
 const user = users.find(u => u.id === parseInt(req.params.id));
 if (!user) return res.status(404).send('User not found');

 const index = users.indexOf(user);
 users.splice(index, 1);

 res.send(user);
});

app.listen(port, () => {
 console.log(`Profile server listening at http://localhost:${port}`);
});
