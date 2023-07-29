function animateButtonClick() {
    const menuButton = document.querySelector('.menu-button');
    menuButton.classList.add('clicked');

    // Remove the 'clicked' class after a short delay to reset the animation
    setTimeout(() => {
        menuButton.classList.remove('clicked');
    }, 200);
}

// Create Animated Circles using JavaScript
const canvas = document.getElementById('shapesCanvas');
const context = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const circleSizes = [30, 50, 70, 90];
const totalCircles = 50;
const animationDuration = 2000; // Duration of each position change animation in milliseconds

function checkOverlap(circle1, circle2) {
    const dx = circle1.x - circle2.x;
    const dy = circle1.y - circle2.y;
    const distance = Math.sqrt(dx * dx + dy * dy);
    return distance < circle1.radius + circle2.radius;
}

function createCircle(className, size) {
    const circle = document.createElement('div');
    circle.classList.add('animated-circle', 'circle', className);
    circle.style.width = `${size}px`;
    circle.style.height = `${size}px`;
    let overlap = true;
    while (overlap) {
        const left = Math.random() * (window.innerWidth - size);
        const top = Math.random() * (window.innerHeight - size);
        circle.style.left = `${left}px`;
        circle.style.top = `${top}px`;
        circle.x = left + size / 2;
        circle.y = top + size / 2;
        circle.radius = size / 2;
        overlap = false;
        const circles = document.querySelectorAll('.animated-circle');
        for (const existingCircle of circles) {
            if (existingCircle !== circle && checkOverlap(circle, existingCircle)) {
                overlap = true;
                break;
            }
        }
    }
    document.body.appendChild(circle);
}

function createWhiteCircle() {
    const circle = document.createElement('div');
    circle.classList.add('animated-circle', 'white-circle');
    circle.style.left = `${Math.random() * window.innerWidth}px`;
    circle.style.top = `${Math.random() * window.innerHeight}px`;
    document.body.appendChild(circle);
}

function moveCircles() {
    const circles = document.querySelectorAll('.animated-circle');
    circles.forEach((circle) => {
        const newX = Math.random() * (window.innerWidth - circle.radius * 2);
        const newY = Math.random() * (window.innerHeight - circle.radius * 2);
        circle.style.transform = `translate(${newX}px, ${newY}px)`;
    });
}

function createCircles() {
    for (let i = 0; i < totalCircles; i++) {
        const randomSizeIndex = Math.floor(Math.random() * circleSizes.length);
        const randomSize = circleSizes[randomSizeIndex];
        createCircle(`circle${i % 4 + 1}`, randomSize);
    }

    for (let i = 0; i < totalCircles / 5; i++) {
        createWhiteCircle();
    }
}

createCircles();

// Continuously move the circles
setInterval(moveCircles, animationDuration);
