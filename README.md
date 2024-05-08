int Lx,Ly,Rx,Ry,bx,by,bxv,byv,brightness,K;
void setting(){
    Lx = 30;
    Ly = 10;
    Rx = 1150;
    Ry = 790;
    bx = width/2;
    by = height/2;
    bxv = 2;
    byv = 1;
    brightness = 100;
    K = 0;
    noCursor();
}
void setup(){
    size(1200, 900);
    background(255, 255, 255);
    colorMode(HSB, 360, 100, 100,1500);
    setting();
}
void draw(){
    background(0, 0, 100);
    ball();
    Rracket();
    Lracket();
}
void Rracket(){
    noStroke();
    fill(240,100,100);
    rect(Rx,Ry,20,100);
    if(keyPressed){
        if (keyCode == UP){
            Ry -= 4;
        }
        else if(keyCode == DOWN){
            Ry += 4;
        }
    }
}
void Lracket(){
    noStroke();
    fill(0,100,100);
    rect(Lx, Ly, 20, 100);
    if (keyPressed){
        if(key == 'w'){
            Ly -= 4;
    }
        if(key == 's'){
            Ly += 4;
    }
 }  
}
   
void ball(){
    noStroke();
    fill(0);
    ellipse(bx,by,10,10);
    bx += bxv;
    by += byv;
    reflection();
    finish();
}
void reflection(){
    if (by >= 895){
        byv *= -1;
    }
    if (by <= 5){
        byv *= -1;
    }
    if (bx+5 >= Rx){
        if (by >= Ry && by <= Ry+100){
        bxv *=-1;
        }
    }
    if (bx-5 <= Lx+20){
        if (by >=Ly && by <= Ly+100){
            bxv *= -1;
        }
    }
}
void finiship(){
    if(brightness ==0){
        textSize(100);
        fill(0);
        text("FINISH",width/2-180,height/2);
        K = 1;
        noLoop();
        textSize(50);
        text("RESTART",100,600);
        text("EXIT",1000,600);
        cursor(ARROW);
    }
}
void finishef(int x){
    if (brightness == 100){
        background(x, 100, 100);
    }
    if (brightness > 0) {
        fill(0,0,100,1500-brightness);  
        ellipse(width/2,height/2,brightness,brightness);
        brightness += 50;
        brightness = brightness % 1500;
    }
}
void finish(){
    if(bx <= 5){
        finishef(240);
        finiship();
    }
    if(bx >= 1195){
        finishef(0);
        finiship();
    }
}
void restart(){
    if(K == 0){
        if(keyCode == ENTER){
        noLoop();
        K = 1;
        background(0,0,100);
        fill(0);
        textSize(100);
        text("RESTART?",width/2-240,height/2);
        textSize(50);
        text("YES",200,600);
        text("NO",1000,600);
        cursor(ARROW);
        }
    }
}
void mousePressed(){
    if(K == 1){
        RorE();
    }
}
void keyPressed(){
    pause();
    restart();
}
void pause(){
    if (keyCode == SHIFT){ //ESCだとタブ自体がきえてゲームが強制終了するから。
        noLoop();
        fill(0);
        textSize(100);
        text("PAUSE",width/2-150,height/2);
        K =2;
    }
    if(K == 2){
        if (key == 'r'){
            loop();
            K = 0;
        }
    }
}
void RorE(){
    float r = dist(mouseX, mouseY, 200, 600);
    float e = dist(mouseX, mouseY,1000,600);
    if(mouseButton == LEFT){
        if(r <= 100){
            setting();
            loop();          
        }
        if (e <= 100) {
            exit();
        }
    }
}
