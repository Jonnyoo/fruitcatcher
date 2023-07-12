# fruitcatcher

	#variables
	app.colorR = 110
	app.colorIncreasing = False
	app.colorGB = 220
	app.steps = 0
	app.mangoSteps = 0
	app.explosionCounter = 0
	app.explosion = False
	app.showEndScreen = False
	app.appleCounter = 0
	app.mangoCounter = 0
	app.pineappleCounter = 0
	app.bombCounter = 0
	app.grapefruitCounter = 0
	app.startScreen = True
	
	#Score and Time Left
	scoreLabel = Label('Score:',40,17,size=20,fill='white',bold=True)
	score = Label(0,75,18,size=20,fill='white',bold=True)
	
	timeLabel = Label('Time Left:',320,17,size=19,fill='white',bold=True)
	time = Label(45,370,17,size=19,fill='white',bold=True)
	
	#Sun
	sunRing = Circle(200, -30, 110)
	sun = Circle(200, -30, 70, fill='gold',opacity=90)
	
	#Ground
	Rect(0,340,400,60,fill='darkGreen')
	Rect(0,345,400,55,fill='green')
	
	#Item Group
	apples = Group()
	mangos = Group()
	itemBomb = Group()
	pineapples = Group()
	grapefruits = Group()
	
	explosions = Group ()
	explosions.nextFill = 'orange'
	
	def drawItems(number):
	    itemX = randrange(20,380)
	    itemY = 0
	    if number == 1:
	        mango = Group(
	            Oval(itemX+4,itemY+10,45,30,rotateAngle=20,fill=gradient
	                ('orange','gold',start='bottom-right')),
	            Oval(itemX,itemY,40,50,rotateAngle=-20,fill=gradient
	                ('orange','gold',rgb(255,247,0),'paleGreen',start='bottom'))
	        )
	        mangos.add(mango)
	    elif number <= 5:
	        apple = Group(
	            Oval(itemX-7,itemY,30,40,fill='crimson'),
	            Oval(itemX+7,itemY,30,40,fill='crimson'),
	            Rect(itemX-2,itemY-28,4,13),
	            Oval(itemX+5,itemY-20,16,7,fill='green',rotateAngle=-25)
	        )
	        apples.add(apple)
	    elif number <= 8:
	        bomb = Group(
	            Polygon(itemX+6,itemY-30,itemX+6,itemY-50,itemX+25,itemY-55,
	                itemX+25,itemY-35,fill=rgb(50,50,50)),
	            Polygon(itemX-6,itemY-30,itemX-6,itemY-50,itemX-25,
	                itemY-55,itemX-25,itemY-35,fill=rgb(50,50,50)),
	            Circle(itemX,itemY+20,20,fill=rgb(90,90,90)),
	            Circle(itemX,itemY-20,20,fill=rgb(90,90,90)),
	            Rect(itemX-3,itemY-55,6,25,fill=rgb(50,50,50)),
	            Rect(itemX-20,itemY-20,40,40,fill=rgb(120,120,120)),
	            Circle(itemX,itemY,17,fill='gold'),
	            Circle(itemX,itemY,14,fill='grey'),
	            Arc(itemX,itemY,21,21,30,60,fill='gold'),
	            Arc(itemX,itemY,21,21,150,60,fill='gold'),
	            Arc(itemX,itemY,21,21,270,60,fill='gold'),
	            Circle(itemX,itemY,5,fill='grey'),
	            Circle(itemX,itemY,3,fill='gold')
	        )
	        itemBomb.add(bomb)
	    elif number <= 11:
	        pineapple = Group(
	            Arc(itemX-13,itemY-36,20,15,260,200,fill=rgb(99,171,69)),
	            Oval(itemX-5,itemY-40,12,35,rotateAngle=-30,fill=rgb(99,171,69)),
	            Oval(itemX,itemY-43,12,35,fill=rgb(99,171,69)),
	            Oval(itemX+5,itemY-40,12,35,rotateAngle=30,fill=rgb(99,171,69)),
	            Arc(itemX+13,itemY-36,20,15,260,200,fill=rgb(99,171,69)),
	            Arc(itemX,itemY,42,85,270,180,fill=rgb(246,167,29)),
	            Circle(itemX,itemY,21,fill=rgb(246,167,29)),
	            Oval(itemX,itemY,42,4,rotateAngle=30,fill=rgb(252,229,129)),
	            Oval(itemX+3,itemY-15,37,4,rotateAngle=30,fill=rgb(252,229,129)),
	            Oval(itemX-5,itemY+15,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	            Oval(itemX-4,itemY-30,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	            
	            Oval(itemX,itemY,42,4,rotateAngle=-30,fill=rgb(252,229,129)),
	            Oval(itemX,itemY-15,37,4,rotateAngle=-30,fill=rgb(252,229,129)),
	            Oval(itemX,itemY+13,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	            Oval(itemX,itemY-30,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	        )
	        pineapple.rotateAngle=15
	        pineapples.add(pineapple)
	    
	    elif number <= 13:
	        grapefruit = Group(
	            Circle(itemX,itemY,25,fill=rgb(241,145,6)),
	            Circle(itemX,itemY,22,fill='white'),
	            Star(itemX,itemY,6,8,fill='white',roundness=70),
	            Star(itemX,itemY,5,8,fill=rgb(171,62,64),roundness=50)
	            )
	        for i in range(8):
	            grapefruitArc = Arc(itemX,itemY,38,38,5+(45*i),35,fill=rgb(206,58,46))
	            grapefruit.add(grapefruitArc)
	        grapefruit.rotateAngle=10
	        grapefruits.add(grapefruit)
	#Clouds
	clouds = Group(
	    Circle(-60,15,35),
	    Circle(-30,15,35),
	    Circle(15,15,35),
	    Circle(70,20,35),
	    Circle(120,15,35),
	    Circle(180,15,35),
	    Circle(220,15,35),
	    Circle(270,15,35),
	    Circle(330,15,35),
	    Circle(380,15,35)
	    )
	
	#score background
	Circle(10,10,6,fill=rgb(40,40,40))
	Circle(110,10,6,fill=rgb(40,40,40))
	Circle(10,25,6,fill=rgb(40,40,40))
	Circle(110,25,6,fill=rgb(40,40,40))
	Rect(4,10,112,15,fill=rgb(40,40,40))
	Rect(10,4,100,27,fill=rgb(40,40,40))
	
	#time background
	Circle(275,10,6,fill=rgb(40,40,40))
	Circle(390,10,6,fill=rgb(40,40,40))
	Circle(275,25,6,fill=rgb(40,40,40))
	Circle(390,25,6,fill=rgb(40,40,40))
	Rect(269,10,127,15,fill=rgb(40,40,40))
	Rect(275,4,114,27,fill=rgb(40,40,40))
	
	#Starting Screen
	#midnightblue = rgb(25,25,107)
	startScreenGroup = Group()
	
	def startScreen():
	    startScreen = Group(
	    Rect(0,0,400,200,fill=rgb(15,15,97)),
	    Rect(0,200,400,140,fill=gradient(rgb(15,15,97),'darkGreen',start='top')),
	    Rect(0,340,400,60,fill='darkGreen'),
	    Rect(0,345,400,55,fill='green'),
	    Circle(20,20,10,fill=rgb(40,40,123)),
	    Circle(380,20,10,fill=rgb(40,40,123)),
	    Circle(20,110,10,fill=rgb(40,40,123)),
	    Circle(380,110,10,fill=rgb(40,40,123)),
	    Rect(20,10,360,110,fill=rgb(40,40,123)),
	    Rect(10,20,380,90,fill=rgb(40,40,123)),
	    Circle(30,30,10,fill=rgb(55,55,137)),
	    Circle(370,30,10,fill=rgb(55,55,137)),
	    Circle(30,100,10,fill=rgb(55,55,137)),
	    Circle(370,100,10,fill=rgb(55,55,137)),
	    Rect(20,30,360,70,fill=rgb(55,55,137)),
	    Rect(30,20,340,90,fill=rgb(55,55,137)),
	    Circle(40,40,10,fill=rgb(75,75,157)),
	    Circle(360,40,10,fill=rgb(75,75,157)),
	    Circle(40,90,10,fill=rgb(75,75,157)),
	    Circle(360,90,10,fill=rgb(75,75,157)),
	    Rect(30,40,340,50,fill=rgb(75,75,157)),
	    Rect(40,30,320,70,fill=rgb(75,75,157)),
	    Label('Fruit Catcher',201,65,size=50,fill='white',bold=True),
	    Label('click anywhere to start',200,275,size=13,fill='white',bold=True),
	    Label('watch out for bombs',200,310,size=13,fill='white',bold=True),
	    Label('Use arrow keys to move in any direction',200,330,size=15,fill='white',bold=True),
	    )
	    startScreenGroup.add(startScreen)
	    #mango
	    startScreenMango = Group(
	    Oval(204,210,45,30,rotateAngle=20,fill=gradient
	        ('orange','gold',start='bottom-right')),
	    Oval(200,200,40,50,rotateAngle=-20,fill=gradient
	        ('orange','gold',rgb(255,247,0),'paleGreen',start='bottom'))
	    )
	    startScreenMango.centerY=210
	    startScreenMango.centerX=130
	    startScreenMango.width+=15
	    startScreenMango.height+=15
	    startScreenGroup.add(startScreenMango)
	    #apple
	    startScreenApple = Group(
	    Oval(193,200,30,40,fill='crimson'),
	    Oval(207,200,30,40,fill='crimson'),
	    Rect(198,172,4,13),
	    Oval(205,180,16,7,fill='green',rotateAngle=-25)
	    )
	    startScreenApple.centerY=205
	    startScreenApple.centerX=270
	    startScreenApple.width+=15
	    startScreenApple.height+=15
	    startScreenGroup.add(startScreenApple)
	    #pineapple
	    startScreenPineapple = Group(
	    Arc(187,164,20,15,260,200,fill=rgb(99,171,69)),
	    Oval(195,160,12,35,rotateAngle=-30,fill=rgb(99,171,69)),
	    Oval(200,157,12,35,fill=rgb(99,171,69)),
	    Oval(205,160,12,35,rotateAngle=30,fill=rgb(99,171,69)),
	    Arc(213,164,20,15,260,200,fill=rgb(99,171,69)),
	    Arc(200,200,42,85,270,180,fill=rgb(246,167,29)),
	    Circle(200,200,21,fill=rgb(246,167,29)),
	    Oval(200,200,42,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(203,185,37,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(195,215,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(196,170,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	
	    Oval(200,200,42,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(200,185,37,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(200,213,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(200,170,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    )
	    startScreenPineapple.centerY=190
	    startScreenPineapple.width+=15
	    startScreenPineapple.height+=15
	    startScreenGroup.add(startScreenPineapple)
	startScreen()
	# Basket
	basket = Rect(180,380,40,10,fill='white')
	
	def endScreen():
	    appleX = 70
	    appleY = 210
	    mangoX = 70
	    mangoY = 277
	    bombX = 180
	    bombY = 250
	    pineappleX = 290
	    pineappleY = 225
	    grapefruitX = 290
	    grapefruitY = 277
	    Rect(0,0,400,400,opacity=50)
	    Rect(50,85,300,230)
	    Rect(30,105,340,190)
	    Circle(50,105,20)
	    Circle(350,105,20)
	    Circle(50,295,20)
	    Circle(350,295,20)
	    
	    #score label
	    Circle(55,110,20,fill=rgb(40,40,40))
	    Circle(345,110,20,fill=rgb(40,40,40))
	    Circle(55,150,20,fill=rgb(40,40,40))
	    Circle(345,150,20,fill=rgb(40,40,40))
	    Rect(35,110,330,40,fill=rgb(40,40,40))
	    Rect(55,90,290,80,fill=rgb(40,40,40))
	    Label(score.value,200,122,size=60,fill='white')
	    Label('SCORE',200,160,size=12,fill='white')
	    
	    #apple
	    Circle(55,195,20,fill=rgb(40,40,40))
	    Circle(55,220,20,fill=rgb(40,40,40))
	    Circle(121,195,20,fill=rgb(40,40,40))
	    Circle(121,220,20,fill=rgb(40,40,40))
	    Rect(35,195,106,25,fill=rgb(40,40,40))
	    Rect(55,175,66,65,fill=rgb(40,40,40))
	    Oval(appleX-7,appleY,28,38,fill='crimson')
	    Oval(appleX+7,appleY,28,38,fill='crimson')
	    Rect(appleX-2,appleY-28,4,13)
	    Oval(appleX+5,appleY-20,15,6,fill='green',rotateAngle=-25)
	    Label(app.appleCounter,115,210,size=30,fill='white')
	    
	    #mango
	    Circle(55,265,20,fill=rgb(40,40,40))
	    Circle(55,290,20,fill=rgb(40,40,40))
	    Circle(121,265,20,fill=rgb(40,40,40))
	    Circle(121,290,20,fill=rgb(40,40,40))
	    Rect(35,265,106,25,fill=rgb(40,40,40))
	    Rect(55,245,66,65,fill=rgb(40,40,40))
	    Oval(mangoX+4,mangoY+10,40,25,rotateAngle=20,fill=gradient
	        ('orange','gold',start='bottom-right'))
	    Oval(mangoX,mangoY,35,45,rotateAngle=-20,fill=gradient
	        ('orange','gold',rgb(255,247,0),'paleGreen',start='bottom'))
	    Label(app.mangoCounter,115,277,size=30,fill='white')
	    
	    #bomb
	    Circle(166,195,20,fill=rgb(140,140,140))
	    Circle(232,195,20,fill=rgb(140,140,140))
	    Circle(166,290,20,fill=rgb(140,140,140))
	    Circle(232,290,20,fill=rgb(140,140,140))
	    Rect(146,195,106,95,fill=rgb(140,140,140))
	    Rect(166,175,66,135,fill=rgb(140,140,140))
	    Polygon(bombX+6,bombY-30,bombX+6,bombY-50,bombX+25,bombY-55,
	        bombX+25,bombY-35,fill=rgb(50,50,50))
	    Polygon(bombX-6,bombY-30,bombX-6,bombY-50,bombX-25,
	        bombY-55,bombX-25,bombY-35,fill=rgb(50,50,50))
	    Circle(bombX,bombY+20,20,fill=rgb(90,90,90))
	    Circle(bombX,bombY-20,20,fill=rgb(90,90,90))
	    Rect(bombX-3,bombY-55,6,25,fill=rgb(50,50,50))
	    Rect(bombX-20,bombY-20,40,40,fill=rgb(120,120,120))
	    Circle(bombX,bombY,17,fill='gold')
	    Circle(bombX,bombY,14,fill='grey')
	    Arc(bombX,bombY,21,21,30,60,fill='gold')
	    Arc(bombX,bombY,21,21,150,60,fill='gold')
	    Arc(bombX,bombY,21,21,270,60,fill='gold')
	    Circle(bombX,bombY,5,fill='grey')
	    Circle(bombX,bombY,3,fill='gold')
	    Label(app.bombCounter,225,250,size=30,fill='white')
	    
	    #pineapple
	    Circle(277,195,20,fill=rgb(40,40,40))
	    Circle(277,220,20,fill=rgb(40,40,40))
	    Circle(343,195,20,fill=rgb(40,40,40))
	    Circle(343,220,20,fill=rgb(40,40,40))
	    Rect(257,195,106,25,fill=rgb(40,40,40))
	    Rect(277,175,66,65,fill=rgb(40,40,40))
	    pineappleTest = Group(
	    Arc(pineappleX-13,pineappleY-36,20,15,260,200,fill=rgb(99,171,69)),
	    Oval(pineappleX-5,pineappleY-40,12,35,rotateAngle=-30,fill=rgb(99,171,69)),
	    Oval(pineappleX,pineappleY-43,12,35,fill=rgb(99,171,69)),
	    Oval(pineappleX+5,pineappleY-40,12,35,rotateAngle=30,fill=rgb(99,171,69)),
	    Arc(pineappleX+13,pineappleY-36,20,15,260,200,fill=rgb(99,171,69)),
	    Arc(pineappleX,pineappleY,42,85,270,180,fill=rgb(246,167,29)),
	    Circle(pineappleX,pineappleY,21,fill=rgb(246,167,29)),
	    Oval(pineappleX,pineappleY,42,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(pineappleX+3,pineappleY-15,37,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(pineappleX-5,pineappleY+15,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	    Oval(pineappleX-4,pineappleY-30,27,4,rotateAngle=30,fill=rgb(252,229,129)),
	    
	    Oval(pineappleX,pineappleY,42,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(pineappleX,pineappleY-15,37,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(pineappleX,pineappleY+13,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    Oval(pineappleX,pineappleY-30,27,4,rotateAngle=-30,fill=rgb(252,229,129)),
	    )
	    pineappleTest.width-=12
	    pineappleTest.height-=28
	    pineappleTest.rotateAngle=20
	    Label(app.pineappleCounter,335,210,size=30,fill='white')
	    
	    #grapefruit
	    Circle(277,265,20,fill=rgb(40,40,40))
	    Circle(277,290,20,fill=rgb(40,40,40))
	    Circle(343,265,20,fill=rgb(40,40,40))
	    Circle(343,290,20,fill=rgb(40,40,40))
	    Rect(257,265,106,25,fill=rgb(40,40,40))
	    Rect(277,245,66,65,fill=rgb(40,40,40))
	    grapefruitTest = Group(
	        Circle(grapefruitX,grapefruitY,25,fill=rgb(241,145,6)),
	        Circle(grapefruitX,grapefruitY,22,fill='white'),
	        Arc(grapefruitX,grapefruitY,38,38,5,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,50,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,95,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,140,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,185,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,230,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,275,35,fill=rgb(206,58,46)),
	        Arc(grapefruitX,grapefruitY,38,38,320,35,fill=rgb(206,58,46)),
	        Star(grapefruitX,grapefruitY,6,8,fill='white',roundness=70),
	        Star(grapefruitX,grapefruitY,5,8,fill=rgb(171,62,64),roundness=50)
	        )
	    grapefruitTest.rotateAngle=10
	    Label(app.grapefruitCounter,335,277,size=30,fill='white')
	    
	def onKeyHold(keys):
	    if 'left' in keys:
	        basket.centerX-=10
	        if basket.right<0:
	            basket.left=400
	    if 'right' in keys:
	        basket.centerX+=10
	        if basket.left>400:
	            basket.right=0
	    if 'up' in keys:
	        basket.centerY-=6
	        if basket.top <348:
	            basket.top=348
	    if 'down' in keys:
	        basket.centerY+=6
	        if basket.bottom>396:
	            basket.bottom=396
	
	def onMousePress(mouseX,mouseY):
	    startScreenGroup.visible=False
	    app.startScreen = False
	
	def onStep():
	    if app.startScreen == False:
	        if app.explosion == True:
	            app.explosionCounter += 1
	            if (app.explosionCounter == 4) or (app.explosionCounter == 8) or (app.explosionCounter == 12) or (app.explosionCounter == 16):
	                if (explosions.nextFill == 'orange'):
	                    explosions.nextFill = 'yellow'
	                else:
	                    explosions.nextFill = 'orange'
	                
	                explosions.add(
	                    Star(basket.centerX, basket.centerY, 10, 10, fill=explosions.nextFill)
	                    )
	        
	            for explosion in explosions.children:
	                explosion.radius+=8
	                if explosion.radius>=120:
	                    explosions.remove(explosion)
	        #time
	        if app.steps==30 and app.showEndScreen==False:
	            app.steps=0
	            if time.value>0:
	                time.value-=1
	            else:
	                app.showEndScreen=True
	                endScreen()
	                app.stop()
	        app.steps+=1
	        
	        #background color and Sun
	        sunRing.fill=gradient('gold',rgb(app.colorR,app.colorGB,app.colorGB))
	        
	        if app.colorIncreasing == True:
	            sunRing.centerY-=1
	            sun.centerY-=1
	        else:
	            sunRing.centerY+=1
	            sun.centerY+=1
	        if app.colorR <= 1:
	            app.colorIncreasing=True
	        if app.colorR>=110:
	            app.colorIncreasing=False
	        if app.colorIncreasing == False:
	            app.colorR -=0.2
	            app.colorGB-=0.4
	        else:
	            app.colorR += 0.2
	            app.colorGB+=0.4
	        app.background = rgb(app.colorR,app.colorGB,app.colorGB)
	        clouds.fill=rgb(app.colorR+145,app.colorR+145,app.colorR+145)
	        
	        #Falling things
	        mangos.centerY+=4
	        apples.centerY+=4
	        itemBomb.centerY+=5
	        pineapples.centerY+=4
	        grapefruits.centerY+=4
	        
	        if app.mangoSteps==10:
	            drawItems(randrange(1,14))
	            app.mangoSteps=0
	        for itemMango in mangos.children:
	            if basket.hitsShape(itemMango) and itemMango.bottom<=basket.bottom:
	                score.value+=30
	                app.mangoCounter+=1
	                mangos.remove(itemMango)
	            elif itemMango.top>400:
	                mangos.remove(itemMango)
	        for itemApple in apples.children:
	            if basket.hitsShape(itemApple) and itemApple.bottom<=basket.bottom:
	                score.value+=5
	                app.appleCounter+=1
	                apples.remove(itemApple)
	            elif itemApple.top>400:
	                apples.remove(itemApple)
	        for bomb in itemBomb.children:
	            if basket.hitsShape(bomb):
	                score.value-=15
	                app.bombCounter+=1
	                app.explosion = True
	                app.explosionCounter=0
	                itemBomb.remove(bomb)
	            elif bomb.top>400:
	                itemBomb.remove(bomb)
	        for itemPineapple in pineapples.children:
	            if basket.hitsShape(itemPineapple) and itemPineapple.bottom<=basket.bottom:
	                score.value+=10
	                app.pineappleCounter +=1
	                pineapples.remove(itemPineapple)
	            elif itemPineapple.top>400:
	                pineapples.remove(itemPineapple)
	        for itemGrapefruit in grapefruits.children:
	            if basket.hitsShape(itemGrapefruit) and itemGrapefruit.bottom<=basket.bottom:
	                score.value+=15
	                app.grapefruitCounter +=1
	                grapefruits.remove(itemGrapefruit)
	            elif itemGrapefruit.top>400:
	                grapefruits.remove(itemGrapefruit)
	        app.mangoSteps+=1
	        
	        #clouds
	        clouds.centerX+=1.5 
	        for cloud in clouds.children:
	            if cloud.left >=400:
	                cloud.right=0
	        
	        
	        #scores
	        score.toFront()
	        score.left = scoreLabel.right+5
	        time.left = timeLabel.right+5
	        scoreLabel.toFront()
        	timeLabel.toFront()
        time.toFront()
