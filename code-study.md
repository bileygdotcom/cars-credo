# Curious:

#238 — показатель спидометра


# Antialias:

#331-335


# SCALE:

#157: var playerW       = SPRITES.PLAYER_STRAIGHT.w * SPRITES.SCALE;

#162: updateCars(dt, playerSegment, playerW);

#188: updateCars(dt, playerSegment, playerW);

#189: if (Util.overlap(playerX, playerW, car.offset, carW, 0.8)) { — Collision

#244: function updateCars(dt, playerSegment, playerW) {

#261: function updateCarOffset(car, carSegment, playerSegment, playerW) {

 #263: var i, j, dir, segment, otherCar, otherCarW, lookahead = 20, carW = car.sprite.w * SPRITES.SCALE;

#272: if ((segment === playerSegment) && (car.speed > speed) && (Util.overlap(playerX, playerW, car.offset, carW, 1.2))) {

#284: otherCarW = otherCar.sprite.w * SPRITES.SCALE;

#353: var n, i, segment, car, sprite, spriteScale, spriteX, spriteY

#395: Render.sprite(ctx, width, height, resolution, roadWidth, sprites, car.sprite, spriteScale, spriteX, spriteY, -0.5, -1, segment.clip);

#400: spriteScale = segment.p1.screen.scale;


