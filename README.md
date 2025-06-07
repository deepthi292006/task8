# task8
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simple Blog Layout</title>
  
  <!-- Bootstrap 5 CSS CDN -->
  <link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
  />
  
  <!-- Font Awesome for social icons -->
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"
  />

  <style>
    body {
      background-color: #f8f9fa;
    }
    footer {
      background-color: #343a40;
      color: white;
    }
    .card img {
      height: 200px;
      object-fit: cover;
    }
  </style>
</head>
<body>

  <!-- Navbar -->
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
      <a class="navbar-brand" href="#">MyBlog</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item"><a class="nav-link active" href="#">Home</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Articles</a></li>
          <li class="nav-item"><a class="nav-link" href="#">About</a></li>
        </ul>
      </div>
    </div>
  </nav>

  <!-- Blog Container -->
  <div class="container py-5">
    <h2 class="mb-4 text-center">Latest Blog Posts</h2>
    <div class="row g-4">

      <!-- Blog Card 1 -->
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <img src="https://source.unsplash.com/400x200/?nature" class="card-img-top" alt="Blog Image">
          <div class="card-body">
            <h5 class="card-title">Post Title One</h5>
            <p class="card-text">This is a short excerpt from the blog post to give readers a quick idea.</p>
            <a href="#" class="btn btn-primary">Read More</a>
          </div>
        </div>
      </div>

      <!-- Blog Card 2 -->
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <img src="https://source.unsplash.com/400x200/?technology" class="card-img-top" alt="Blog Image">
          <div class="card-body">
            <h5 class="card-title">Post Title Two</h5>
            <p class="card-text">Another brief summary that highlights the content of the post for easy scanning.</p>
            <a href="#" class="btn btn-primary">Read More</a>
          </div>
        </div>
      </div>

      <!-- Blog Card 3 -->
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <img src="https://source.unsplash.com/400x200/?coding" class="card-img-top" alt="Blog Image">
          <div class="card-body">
            <h5 class="card-title">Post Title Three</h5>
            <p class="card-text">Interesting insights about web development, trends, or tutorials.</p>
            <a href="#" class="btn btn-primary">Read More</a>
          </div>
        </div>
      </div>

    </div>
  </div>

  <!-- Footer -->
  <footer class="text-center py-4">
    <div class="container">
      <p class="mb-2">Connect with us:</p>
      <a href="#" class="text-white me-3"><i class="fab fa-facebook fa-lg"></i></a>
      <a href="#" class="text-white me-3"><i class="fab fa-twitter fa-lg"></i></a>
      <a href="#" class="text-white me-3"><i class="fab fa-instagram fa-lg"></i></a>
      <a href="#" class="text-white"><i class="fab fa-github fa-lg"></i></a>
      <p class="mt-3 mb-0">&copy; 2025 MyBlog. All rights reserved.</p>
    </div>
  </footer>

  <!-- Bootstrap 5 JS CDN -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
npx create-strapi-app my-blog-api --quickstart

http://localhost:1337/api/posts?populate=*

<script>
  const container = document.querySelector(".row");

  async function loadPosts() {
    try {
      const res = await fetch("http://localhost:1337/api/posts?populate=*");
      const data = await res.json();

      container.innerHTML = ""; // Clear placeholder

      data.data.forEach(post => {
        const { title, description, image } = post.attributes;
        const imgUrl = image.data ? image.data.attributes.url : 'https://via.placeholder.com/400x200';

        container.innerHTML += `
          <div class="col-md-4">
            <div class="card h-100 shadow-sm">
              <img src="http://localhost:1337${imgUrl}" class="card-img-top" alt="${title}">
              <div class="card-body">
                <h5 class="card-title">${title}</h5>
                <p class="card-text">${description}</p>
                <a href="#" class="btn btn-primary">Read More</a>
              </div>
            </div>
          </div>`;
      });

    } catch (err) {
      console.error("Error loading posts:", err);
      container.innerHTML = `<p class="text-danger">Failed to load blog posts.</p>`;
    }
  }

  loadPosts();
</script>
