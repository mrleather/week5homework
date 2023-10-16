# week5homeworkPImage img;
float s;
int count;
void setup() {
  size(1080, 1080);
  background(255);
  noStroke();
  img = loadImage("smart.jpg");
}
void draw() {
  background(255);
  s = map(mouseX, 0, width, 1, 100);
  for (int y = 0; y < img.height; y+=s ) {
    for (int x = 0; x < img.width; x+=s) {
      int loc = x + (y * img.width);
      rectMode(CENTER);
      float bri=brightness(img.pixels[loc]);
      if (x%2==0) {
        moveB (bri, s, x, y);
      } else {

        moveA(bri, x-s, y, x-s, y-s);
      }
    }
  }
}

void moveB(float bri, float kuan, int rectx, int recty) {
  int iter=int(map(bri, 0, 255, 10, 0));
  if (iter>0) {
    float interval=kuan/(iter*2);
    for (int i=0; i<iter; i++) {
      float rectsize=kuan-interval*i*2;
      noFill();
      stroke(0);
      strokeWeight(1);
      rect(rectx, recty, rectsize, rectsize);
    }
  }
}
void mousePressed() {
  save("smart.jpg");
}
void  moveA(float bri, float x1, float y1, float x2, float y2) {
  int weight=int(map(bri, 100, 255, 10, 1));
  float s1=s;
  if (weight>0) {
    float interval=s1/weight;
    for (int i=0; i<=s1; i=i+1) {
      strokeWeight(1);
      stroke(0);
      line(x1+i*interval, y1, x2+i*interval, y2);
    }
  }
}
