# Мои Заметки

## масштаб

1. В common.js (сейчас строка 413) лежит определение для масштаба спрайтов. Я заменил **PLAYER_STRAIGHT.w**, потому что играюсь с масштабом машины игрока:

`//SPRITES.SCALE = 0.3 * (1/SPRITES.PLAYER_STRAIGHT.w) // the reference sprite width should be 1/3rd the (half-)roadWidth`
`SPRITES.SCALE = 0.3 * (1/80)`

2. в *common.js:*
`player: function(1.ctx, 2.width, 3.height, 4.resolution, 5.roadWidth, 6.sprites, 7.speedPercent, 8.scale, 9.destX, 10.destY, 11.steer, 12.updown)`

3. в *v4.final.html*
`if (segment == playerSegment) {`
          `Render.player(1.ctx, 2.width, 3.height, 4.resolution, 5.roadWidth, 6.sprites, 7.speed/maxSpeed,`
                        `8.cameraDepth/playerZ,` - важнейшее место
                        `9.width/2,`
                        `10.(height/2) - (cameraDepth/playerZ * Util.interpolate(playerSegment.p1.camera.y,` `playerSegment.p2.camera.y, playerPercent) * height/2),`
                        `11.speed * (keyLeft ? -1 : keyRight ? 1 : 0),`
                        `12.playerSegment.p2.world.y - playerSegment.p1.world.y);`

4. т.е. масштаб, который приходит в common.js:
scale = cameraDepth/playerZ, где:
cameraDepth = 1 / Math.tan((fieldOfView/2) * Math.PI/180);
playerZ     = (cameraHeight * cameraDepth);
=> scale = _cameraDepth_/(cameraHeight * _cameraDepth_) = 1/cameraHeight
=> scale = 1/cameraHeight

5. index4 - получилось увеличить масштаб спрайтов окружения отдельно от машин! #398-403
Добавил множитель масштаба 2 в строку "Render.sprite"
for(i = 0 ; i < segment.sprites.length ; i++) {
          sprite      = segment.sprites[i];
          spriteScale = segment.p1.screen.scale;
          spriteX     = segment.p1.screen.x + (spriteScale * sprite.offset * roadWidth * width/2);
          spriteY     = segment.p1.screen.y;
          Render.sprite(ctx, width, height, resolution, roadWidth, sprites, sprite.source, 2*spriteScale, spriteX, spriteY, (sprite.offset < 0 ? -1 : 0), -1, segment.clip);



## максималка

1. Регулировка максимальной скорости работает, однако слишком сильное увеличение скорости может привести к проблемам с определением коллизий v4.final.html:
`var maxSpeed  = segmentLength/step*1.5;`

2. Нужно затестить. Фактор 1,5 даёт очень аццкую динамику, но нужно тестить коллизии