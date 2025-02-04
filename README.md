# James1coder

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CineVerse - Entertainment Hub</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        :root {
            --primary-color: #e50914;
            --dark-color: #141414;
            --light-color: #f4f4f4;
        }

        body {
            background-color: var(--dark-color);
            color: var(--light-color);
        }

        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            display: flex;
            justify-content: space-between;
            padding: 20px 50px;
            background: linear-gradient(180deg, rgba(0,0,0,0.8) 0%, rgba(0,0,0,0) 100%);
            z-index: 1000;
        }

        .logo {
            color: var(--primary-color);
            font-size: 2rem;
            font-weight: bold;
        }

        .nav-links {
            display: flex;
            gap: 25px;
        }

        .nav-links a {
            color: var(--light-color);
            text-decoration: none;
            transition: color 0.3s;
        }

        .nav-links a:hover {
            color: var(--primary-color);
        }

        .hero {
            height: 100vh;
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)),
                        url('https://source.unsplash.com/random/1920x1080/?movie') center/cover;
            display: flex;
            align-items: center;
            padding: 0 50px;
        }

        .hero-content {
            max-width: 600px;
        }

        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
        }

        .hero p {
            font-size: 1.2rem;
            margin-bottom: 30px;
        }

        .cta-btn {
            padding: 15px 30px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.1rem;
        }

        .content-section {
            padding: 50px;
        }

        .section-title {
            margin-bottom: 30px;
        }

        .movies-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
        }

        .movie-card {
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            transition: transform 0.3s;
        }

        .movie-card:hover {
            transform: scale(1.05);
        }

        .movie-card img {
            width: 100%;
            height: 300px;
            object-fit: cover;
        }

        .movie-info {
            position: absolute;
            bottom: 0;
            background: linear-gradient(transparent, rgba(0,0,0,0.9));
            padding: 20px;
            width: 100%;
        }

        footer {
            background-color: #000;
            padding: 50px;
            text-align: center;
        }

        .social-links {
            margin-bottom: 20px;
        }

        .social-links a {
            color: white;
            margin: 0 10px;
            font-size: 1.5rem;
        }

        @media (max-width: 768px) {
            .navbar {
                padding: 15px 20px;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .content-section {
                padding: 30px 20px;
            }
        }
    </style>
</head>
<body>
    <nav class="navbar">
        <div class="logo">CineVerse</div>
        <div class="nav-links">
            <a href="#home">Home</a>
            <a href="#movies">Movies</a>
            <a href="#tv">TV Shows</a>
            <a href="#my-list">My List</a>
        </div>
    </nav>

    <section class="hero" id="home">
        <div class="hero-content">
            <h1>Unlimited Entertainment</h1>
            <p>Stream thousands of movies and TV shows anytime, anywhere.</p>
            <button class="cta-btn">Get Started</button>
        </div>
    </section>

    <section class="content-section" id="movies">
        <h2 class="section-title">Popular Movies</h2>
        <div class="movies-grid" id="movies-container"></div>
    </section>

    <section class="content-section" id="tv">
        <h2 class="section-title">TV Shows</h2>
        <div class="movies-grid" id="tv-container"></div>
    </section>

    <footer>
        <div class="social-links">
            <a href="#"><i class="fab fa-facebook"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-instagram"></i></a>
        </div>
        <p>&copy; 2023 CineVerse. All rights reserved.</p>
    </footer>

    <script>
        // Sample movie data (replace with API data)
        const movies = [
            { title: 'Movie 1', image: 'https://source.unsplash.com/random/300x450/?movie-poster' },
            { title: 'Movie 2', image: 'https://source.unsplash.com/random/300x450/?film' },
            { title: 'Movie 3', image: 'https://source.unsplash.com/random/300x450/?cinema' },
            { title: 'Movie 4', image: 'https://source.unsplash.com/random/300x450/?poster' },
            { title: 'Movie 5', image: 'https://source.unsplash.com/random/300x450/?movie' },
            { title: 'Movie 6', image: 'https://source.unsplash.com/random/300x450/?horror' },
        ];

        const tvShows = [
            { title: 'TV Show 1', image: 'https://source.unsplash.com/random/300x450/?tv-show' },
            { title: 'TV Show 2', image: 'https://source.unsplash.com/random/300x450/?series' },
            { title: 'TV Show 3', image: 'https://source.unsplash.com/random/300x450/?drama' },
            { title: 'TV Show 4', image: 'https://source.unsplash.com/random/300x450/?comedy' },
            { title: 'TV Show 5', image: 'https://source.unsplash.com/random/300x450/?sci-fi' },
            { title: 'TV Show 6', image: 'https://source.unsplash.com/random/300x450/?fantasy' },
        ];

        function createMediaCard(media) {
            return `
                <div class="movie-card">
                    <img src="${media.image}" alt="${media.title}">
                    <div class="movie-info">
                        <h3>${media.title}</h3>
                    </div>
                </div>
            `;
        }

        document.addEventListener('DOMContentLoaded', () => {
            const moviesContainer = document.getElementById('movies-container');
            const tvContainer = document.getElementById('tv-container');

            movies.forEach(movie => {
                moviesContainer.innerHTML += createMediaCard(movie);
            });

            tvShows.forEach(show => {
                tvContainer.innerHTML += createMediaCard(show);
            });
        });

        // Smooth scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            if (window.scrollY > 100) {
                document.querySelector('.navbar').style.background = '#000';
            } else {
                document.querySelector('.navbar').style.background = 'linear-gradient(180deg, rgba(0,0,0,0.8) 0%, rgba(0,0,0,0) 100%)';
            }
        });
    </script>
</body>
</html>
```
