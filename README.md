# insta
insta.js

const express = require('express');
const app= express();

const mongoose = require('mongoose');
app.use(express.json());

const postSchema = new mongoose.Schema({
    image:String,
    caption:String,
    comments:{
        type:[String],
        default:[]
    },
    likes:{
        type : Number,
        default:0
    }
});

const post= mongoose.model('post', postSchema);

app.get('/posts', async (req, res) => {
    const posts = await post.find({});
    res.send(posts);
});

app.get('/posts/:postId', async (req, res) => {
    const id = req.params.postId;

    const post = await post.findById(IDBRequest);
    res.send(posts);
});

app.post('/posts', async (req, res) => {


    const image= req.body.image;
    const caption = req.body.caption;

    const post = new Post({
        image:image,
        caption:caption
        
    });

    await post.save();

    res.send(posts);
});

app.put('/posts/:id', async (req, res) => {
    const id = req.params.id;
    const caption = req.body.caption;
    
    const post = await post.findById(id);

    post.caption = caption;

    await post.save();

    res.send(post);
}); 

app.delete('/post/:id', async (req, res) => {
    const id = req.params.id;
    
     await post.findByIdAndDelete(id);
     res.send('post deleted successfully');
});

app.put('/posts/:id/likes', async (req, res) => {

    const id = req.params.id;

    const post = await post.findById(id);

    post.likes = post.likes + 1;

    await post.save();

    res.send(post);
}); 

app.put('/posts/:id/unlike', async (req, res) => {

    const id = req.params.id;

    const post = await post.findById(id);

    post.likes = post.likes - 1;

    await post.save();

    res.send(post);
}); 
app.put('/posts/:id/comment', async (req, res) => {

    const id = req.params.id;
    const comment = req.body.comment;
    const post = await post.findById(id);

    post.comments.push(comment);

    await post.save();

    res.send(post);
}); 

app.get('/posts/:id/comments', async (req, res) => {

    const id = req.params.id;

    const post = await post.findById(id);
    res.send(post.comments);

});

app.get('/posts/:id/likes', async (req, res) => {

    const id = req.params.id;

    const post = await post.findById(id);
    res.send(post.likes);
    
});

app.listen(3000, () => {
    console.log('server started on port 3000');
    mongoose.connect("mongodb+srv://bavishyakotamreddy22:BUOUQpdnnqeo0Hwx@cluster0.gmvu8cd.mongodb.net/").then(() => {
        console.log("Connected to the database!");
    })
})




        





