[TOC]

# fuchsia.game.tennis


## **PROTOCOLS**

## TennisService {#TennisService}
*Defined in [fuchsia.game.tennis/tennis.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.game.tennis/tennis.fidl#8)*


### GetState {#GetState}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#GameState'>GameState</a></code>
            </td>
        </tr></table>

### RegisterPaddle {#RegisterPaddle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>paddle</code></td>
            <td>
                <code><a class='link' href='#Paddle'>Paddle</a></code>
            </td>
        </tr></table>



## Paddle {#Paddle}
*Defined in [fuchsia.game.tennis/tennis.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.game.tennis/tennis.fidl#26)*


### NewGame {#NewGame}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>is_player_2</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Up {#Up}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Down {#Down}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Stop {#Stop}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### GameState {#GameState}
*Defined in [fuchsia.game.tennis/tennis.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.game.tennis/tennis.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ballX</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ballY</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_1_y</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_2_y</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_1_score</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_2_score</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>game_num</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_1_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>player_2_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













