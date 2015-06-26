#Elo Rating PHP
A PHP class which implements the [Elo rating system](http://en.wikipedia.org/wiki/Elo_rating_system).
#[database](http://stackoverflow.com/a/26043945/5053726)    
Basically, there will be two tables: players(name,whatever else,rating) and games(player_id_white,player_id_black,result=1,0,-1,date).  

After a game has been deleted, reset all players' ratings back to the initial value and recalculate them from scratch. Just read the games table sorted by date, update ratings in memory and finally write them back to the players table.  

This is somehow straightforward and crude solution, but should work for you unless (until) you have thousands of players and millions of games.  


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
