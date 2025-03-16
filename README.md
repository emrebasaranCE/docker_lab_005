## Docker Lab 5
In this example, we create networks and manage the communications of the containers. We first need to create a network for our containers:

    docker network create favorites-network

For our app to communicate with mongo database, we need to give the container name in our app.js file:

    'mongodb://mongodb:27017/swfavorites', // app.js in line 71 

Now we run mongo database with the network arguments:
    
    docker run \ 
        -d --rm --name mongodb \
        --network favorites-network \
        mongo

And then we build our node app:
    
    docker build -t favorites-node .

And run our node app

    docker run --name favorites \
        -d --rm -p 3000:3000 \
        --network favorites-network \
        favorites-node

And at this point, if we look into the `localhost:3000/favorites` we get this result:

    {
        "favorites":[]
    }

And this output shows us that our containers can communicate via the network we just created. 