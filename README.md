<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        html, body {
            margin: 0; 
            padding: 0; 
            overflow: hidden; 
            width: 100%; 
            height: 100%;
            display: flex; 
            justify-content: center; 
            align-items: center;
            background: transparent;
        }

        .carousel-container {
            width: 100%; max-width: 450px; 
            aspect-ratio: 1 / 1; 
            position: relative;
            background-color: #000;
            border-radius: 8px;
            overflow: hidden;
        }

        .carousel-track {
            display: flex; 
            width: 100%; 
            height: 100%;
            transition: transform 0.4s cubic-bezier(0.215, 0.61, 0.355, 1);
        }

        .carousel-track img {
            width: 100%; 
            height: 100%;
            flex-shrink: 0; 
            object-fit: cover; 
            display: block;
        }

        .carousel-arrow {
            position: absolute; 
            top: 50%; 
            transform: translateY(-50%);
            background-color: rgba(255, 255, 255, 0.8); 
            color: #262626;
            border: none; 
            padding: 8px; 
            cursor: pointer; 
            z-index: 10;
            font-size: 1.2rem; 
            border-radius: 50%; 
            width: 32px; 
            height: 32px;
            display: flex; 
            justify-content: center; 
            align-items: center;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .carousel-arrow.left { left: 10px; }
        .carousel-arrow.right { right: 10px; }
        .carousel-arrow:disabled { display: none; }

        .carousel-dots {
            position: absolute; bottom: 12px; left: 50%;
            transform: translateX(-50%);
            display: flex; gap: 6px; z-index: 10;
        }

        .dot {
            width: 6px; height: 6px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%; cursor: pointer; transition: background 0.3s;
        }

        .dot.active {
            background-color: #fff;
            transform: scale(1.2);
        }
    </style>
</head>
<body>

    <div class="carousel-container">
        <div class="carousel-track">
            <img src="pic1.png" alt="1">
            <img src="pic2.png" alt="2">
            <img src="pic3.png" alt="3">
            <img src="pic4.png" alt="4">
            <img src="pic5.png" alt="5">
            <img src="pic6.png" alt="6">
            <img src="pic7.png" alt="7">
        </div>

        <button class="carousel-arrow left" disabled><i class="fas fa-chevron-left"></i></button>
        <button class="carousel-arrow right"><i class="fas fa-chevron-right"></i></button>

        <div class="carousel-dots" id="dotContainer"></div>
    </div>

    <script>
        const track = document.querySelector('.carousel-track');
        const images = Array.from(track.querySelectorAll('img'));
        const leftArrow = document.querySelector('.carousel-arrow.left');
        const rightArrow = document.querySelector('.carousel-arrow.right');
        const dotContainer = document.getElementById('dotContainer');

        let currentIndex = 0;

        images.forEach((_, i) => {
            const dot = document.createElement('div');
            dot.classList.add('dot');
            if (i === 0) dot.classList.add('active');
            dot.addEventListener('click', () => updateCarousel(i));
            dotContainer.appendChild(dot);
        });

        const dots = Array.from(document.querySelectorAll('.dot'));

        const updateCarousel = (index) => {
            track.style.transform = `translateX(-${index * 100}%)`;
            currentIndex = index;

            leftArrow.disabled = currentIndex === 0;
            rightArrow.disabled = currentIndex === images.length - 1;

            dots.forEach(dot => dot.classList.remove('active'));
            dots[currentIndex].classList.add('active');
        };

        rightArrow.addEventListener('click', () => updateCarousel(currentIndex + 1));
        leftArrow.addEventListener('click', () => updateCarousel(currentIndex - 1));
    </script>
</body>
</html>
