# PROJECT 3: MERN STACK IMPLEMENTATION

## Step 1: Backend configuration

### Installing nodejs

Commands:

sudo apt update

sudo apt upgrade

curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -

sudo apt-get install -y nodejs

node -v

npm -v

mkdir Todo

ls

cd Todo

npm init

ls

![backend-configuration1](https://user-images.githubusercontent.com/111616140/210492061-337921da-db90-424c-96bc-5a680e1988ee.jpg)

![backend-configuration2](https://user-images.githubusercontent.com/111616140/210492080-5ab96e12-3f9f-42c3-a107-1b0e076bff8a.jpg)

![backend-configuration3](https://user-images.githubusercontent.com/111616140/210492092-081c1d0f-fa2c-4bf4-9394-0c93846d9f43.jpg)

![backend-configuration4](https://user-images.githubusercontent.com/111616140/210492114-a8cceb90-2f09-4c36-aba1-26ae61fc07c3.jpg)

![backend-configuration5](https://user-images.githubusercontent.com/111616140/210492138-ee454a7e-58fd-4fa7-b05e-6a0548357b7c.jpg)

### Installing expressjs

Commands:

npm install express

touch index.js

ls

npm install dotenv

vim index.js

node index.js

mkdir routes

cd routes

touch api.js

vim api.js

![installing-expreesjs1](https://user-images.githubusercontent.com/111616140/211180417-5bd8ac6a-9265-4914-a401-8d2aca4c91f6.jpg)

![testing-expressjs-on-web](https://user-images.githubusercontent.com/111616140/211180421-6a0b0222-a2e6-4c63-ab0a-d9ffd311fdf3.jpg)

![installing-expreesjs2](https://user-images.githubusercontent.com/111616140/211180427-ca480e2f-6c16-4d0e-bbd1-147815228785.jpg)

### Models

Commands

npm install mongoose

mkdir models

cd models

touch todo.js

vim todo.js

cd ~

cd routes

vim api.js

![models](https://user-images.githubusercontent.com/111616140/211181207-aea8a5dc-cb33-4bc4-96e2-d4b8c9ca1638.jpg)

### MongoDB database

We set up our MongDB account and created a cluster

Commands:

touch .env

vi .env

vim index.js

![MongoDB-1](https://user-images.githubusercontent.com/111616140/211236673-bf725691-1779-4a8a-b403-cfd23bf27ad0.jpg)


node index.js

![testing-backend-from-terminal](https://user-images.githubusercontent.com/111616140/213346315-322a9cce-ec98-4d3d-8754-2e7d01a88720.jpg)

Next, I install postman to help test and share my APIs to successfully complete my backend creation. I then test it by executing  POST and GET requests.

![post-request-on-postman](https://user-images.githubusercontent.com/111616140/213347306-f1a82fde-d397-4384-b8b4-054cbf814766.jpg)

![get-request-on-postman](https://user-images.githubusercontent.com/111616140/213347344-f7539422-525b-46d9-a5e6-ff380d4cd8ce.jpg)

## Step 2: Frontend Creation

Commands:

npx create-react-app client

We then install some dependencies as well;

npm install concurrently --save-dev

npm install nodemon --save-dev

cd client

vi package.json

We then open port 5000 to be able to access the application directly from the browser

npm run dev

cd client

cd src

mkdir components

cd components

touch Input.js ListTodo.js Todo.js

vi Input.js

We replace the default script with that provided in the dcoumentation

cd ../..

npm install axios

cd src/components

vi ListTodo.js

We replace the default script with that provided in the dcoumentation

vi Todo.js

We replace the default script with that provided in the dcoumentation

cd ..

vi App.js

We replace the default script with that provided in the dcoumentation

vi App.css

vim index.css

cd ../..

npm run dev

![front-end-creation-1](https://user-images.githubusercontent.com/111616140/215236997-9e97e52e-16f0-476d-a80f-87cc059c74dd.jpg)

![front-end-creation-2](https://user-images.githubusercontent.com/111616140/215237005-4e965e9b-b1af-4041-8da5-61c3a6bb8c1b.jpg)

![front-end-creation-3](https://user-images.githubusercontent.com/111616140/215237011-ed83f05a-c6d7-43de-b7a1-fb8c14bc476f.jpg)

![front-end-creation-4](https://user-images.githubusercontent.com/111616140/215237027-8c9e5a9f-0f27-4526-b93a-336cb8f13fb7.jpg)

![front-end-creation-5](https://user-images.githubusercontent.com/111616140/215237054-1b4c3ada-3aa2-4eed-8fec-1381399cfbab.jpg)

![front-end-creation-6](https://user-images.githubusercontent.com/111616140/215237063-3a0f01e9-1bdc-48e8-8013-a0074ef9ac02.jpg)

![front-end-creation-7](https://user-images.githubusercontent.com/111616140/215237076-8e6c830b-8f80-40dc-b71f-0a38dddfcf1e.jpg)

![front-end-creation-8](https://user-images.githubusercontent.com/111616140/215237144-8e4347a4-1112-4c0c-bcb0-9fd293a9b176.jpg)

![front-end-creation-9](https://user-images.githubusercontent.com/111616140/215237152-e3c91e21-b8f7-4f94-bca5-f853c35127e4.jpg)
