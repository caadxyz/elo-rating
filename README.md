#Elo Rating PHP
A PHP class which implements the [Elo rating system](http://en.wikipedia.org/wiki/Elo_rating_system).
#database    
Basically, there will be two tables: players(name,whatever else,rating) and games(player_id_white,player_id_black,result=1,0,-1,date).  

After a game has been deleted, reset all players' ratings back to the initial value and recalculate them from scratch. Just read the games table sorted by date, update ratings in memory and finally write them back to the players table.  

This is somehow straightforward and crude solution, but should work for you unless (until) you have thousands of players and millions of games.  

http://stackoverflow.com/a/26043945/5053726

#initialization(K-value)   
http://stackoverflow.com/a/26043945/5053726  
在美国西洋棋联盟（USCF）的排名中，主要採用三级制，根据参赛者的实力值，分成三个领域来决定K-value：   
* 实力值0-2099者，K-value为32； 
* 实力值2100-2399者，K-value为24； 
* 实力值 >=2400者，K-value为16。 

为甚麽业馀级别的K-value需要高一点呢？ 
有一种说法是避免偶发性的失算，例如一个人的实力值约有2500，但初始实力值是1600的话，升级至应有积分便需要对赛很多局。调整K-value的话能加速达到应有的等级领域。  

为了让刚加入系统的高手尽快得到应有的评级，世界西洋棋联盟（FIDE）索性让新加入者使用一个较高的K-value，在30局过后才降回一般水平。

FIDE对K值的设定如下：  
* 首30局，K-value为25； 
* 实力值不足2400的，K-value为15； 
* 实力值到达2400并已进行超过30局的，K-value为10。以后K-value不会再改变。 


#Usage

    require 'src/Rating/Rating.php';

    // player A elo = 1000
    // player B elo = 2000
    // player A lost
    // player B win
    
    $rating = new Rating(1000, 2000, 0, 1);

    // player A elo = 1000
    // player B elo = 2000
    // player A draw
    // player B draw
    
    $rating = new Rating(1000, 2000, .5, .5);
    
    $results = $rating->getNewRatings();
    
    echo "New rating for player A: " . $results['a'];
    echo "New rating for player B: " . $results['b'];
    
---------------------------------------

#Credits
    
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Elo Rating PHP</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://michalchovanec.com" property="cc:attributionName" rel="cc:attributionURL">Michal Chovanec</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
