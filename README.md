# agrinho
projeto do alura
let turtle;

let trashItems = [];

let score = 0;

function setup() {

  createCanvas(600, 400);

  turtle = new Turtle();

  // Generate random trash items

  for (let i = 0; i < 15; i++) {

    trashItems.push(new Trash());

  }

}

function draw() {

  background(0, 150, 200); // Ocean blue background

  // Show and move the turtle

  turtle.show();

  turtle.move();

  // Show and move trash items

  for (let i = trashItems.length - 1; i >= 0; i--) {

    trashItems[i].show();

    trashItems[i].move();

    // Check collision with the turtle

    if (trashItems[i].hits(turtle)) {

      trashItems.splice(i, 1);

      score += 5; // Points for each collected trash

    }

  }

  // If all trash is collected, generate more

  if (trashItems.length === 0) {

    for (let i = 0; i < 15; i++) {

      trashItems.push(new Trash());

    }

  }

  // Display score

  fill(255);

  textSize(16);

  text('Trash Collected: ' + score, 10, 20);

}

// Turtle class

class Turtle {

  constructor() {

    this.x = width / 2;

    this.y = height - 50;

    this.size = 40;

  }

  show() {

    fill(34, 139, 34);

    ellipse(this.x, this.y, this.size, this.size);

    // Optional: add details to resemble a turtle

  }

  move() {

    if (keyIsDown(LEFT_ARROW) && this.x - this.size / 2 > 0) {

      this.x -= 5;

    }

    if (keyIsDown(RIGHT_ARROW) && this.x + this.size / 2 < width) {

      this.x += 5;

    }

  }

}

// Trash class

class Trash {

  constructor() {

    this.x = random(width);

    this.y = random(-100, -40);

    this.size = 20;

    this.speed = random(2, 4);

  }

  show() {

    fill(139, 69, 19);

    rect(this.x, this.y, this.size, this.size);

  }

  move() {

    this.y += this.speed;

    if (this.y > height + this.size) {

      this.y = random(-100, -40);

      this.x = random(width);

    }

  }

  hits(turtle) {

    let d = dist(this.x + this.size / 2, this.y + this.size / 2, turtle.x, turtle.y);

    return d < (this.size + turtle.size) / 2;

  }

}
