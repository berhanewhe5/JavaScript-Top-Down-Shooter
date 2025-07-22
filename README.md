# Top-Down Zombie Shooter Game

This project is a top-down 2D zombie survival game where the player must fend off waves of zombies using a shotgun. Players can move, aim, shoot, and survive for as long as possible while trying to achieve a high score. The game uses basic 2D graphics and animations to provide an engaging and dynamic experience.

<img src="https://github.com/user-attachments/assets/94b4a62e-39e7-489c-8d99-fcd3b9acc6a6" alt="Screenshot 1" width="400">
<img src="https://github.com/user-attachments/assets/a1819c6f-8e08-4d76-b265-ae6f945225b6" alt="Screenshot 2" width="400">
<img src="https://github.com/user-attachments/assets/06ec32b8-4a16-4067-bc27-4e483e7e0421" alt="Screenshot 3" width="400">
<img src="https://github.com/user-attachments/assets/03396b12-17c6-4aa4-ba44-1c4c74786699" alt="Screenshot 4" width="400">


## Features

- **Player Movement**: Move forward and backward while rotating the character using the mouse.
- **Shooting**: Aim with the mouse and shoot bullets to kill zombies.
- **Infinite Grass**: Dynamic background with endless grass terrain as the player moves.
- **Zombies**: Spawn, chase, and attack the player with animated zombie sprites.
- **Animations**: Player and zombie have idle, movement, and attack animations.
- **Crosshair**: Dynamic crosshair follows mouse movement.
- **Score System**: Track current score and high score.
- **Game Over Screen**: Display high score after the game ends.
- **Responsive Controls**: Supports mouse controls for shooting and keyboard controls for movement.

## Gameplay

- Move the player using `W`, `A`, `S`, `D` or the arrow keys.
- Aim with the mouse.
- Left-click to shoot at zombies.
- Survive as long as possible and try to achieve the highest score.
- When hit by a zombie, the game ends and shows the "Game Over" screen with the player's high score.

## Controls

- **Move Forward**: `W` / `Up Arrow`
- **Move Backward**: `S` / `Down Arrow`
- **Move Left**: `A` / `Left Arrow`
- **Move Right**: `D` / `Right Arrow`
- **Shoot**: `Left Mouse Button`
- **Aim**: Mouse movement

## Assets

The game uses sprite sheets for both player and zombie animations:
- **Player animations**: Idle, move, and shoot with a shotgun.
- **Zombie animations**: Movement and attack animations.

### Images
- **Player Sprite**: `images/Top_Down_Survivor/shotgun/idle/`
- **Zombie Sprite**: `images/tds_zombie/export/`
- **Grass Background**: `images/grass.png`
- **Bullet**: `images/bullet.png`
- **Crosshair**: `images/crosshair097.png`
- **Game Over Screen**: `images/Game Over.png`

## Installation and Setup

1. Clone or download the repository.
2. Open the index.html file in a browser.
3. Start the game by interacting with the canvas.

## Link to the game

Link to the game online: https://berhanewhe5.github.io/JavaScript-Top-Down-Shooter/

## Credits

1. All Code by Berhane Wheeler
2. Zombie sprite: https://opengameart.org/content/animated-top-down-zombie
3. Player sprite: https://opengameart.org/content/animated-top-down-survivor-player
4. Grass sprite: https://opengameart.org/content/grass-texture-pack

5. ERROR in ./src/CompareEmployees.tsx:15:36
TS2365: Operator '+' cannot be applied to types '{}' and 'number'.
    13 |       emp.events?.forEach((event) => {
    14 |         if (event.rsvped) {
  > 15 |           eventMap.set(event.name, (eventMap.get(event.name) || 0) + 1);
       |                                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    16 |         }
    17 |       });
    18 |     });

ERROR in ./src/CompareEmployees.tsx:20:18
TS2345: Argument of type '{ name: unknown; count: unknown; }[]' is not assignable to parameter of type 'SetStateAction<never[]>'.
  Type '{ name: unknown; count: unknown; }[]' is not assignable to type 'never[]'.
    Type '{ name: unknown; count: unknown; }' is not assignable to type 'never'.
    18 |     });
    19 |     const chartData = Array.from(eventMap.entries()).map(([name, count]) => ({ name, count }));
  > 20 |     setTopEvents(chartData);
       |                  ^^^^^^^^^
    21 |   }, []);
    22 |
    23 |   const findCommonalities = (id) => {

ERROR in ./src/CompareEmployees.tsx:23:30
TS7006: Parameter 'id' implicitly has an 'any' type.
    21 |   }, []);
    22 |
  > 23 |   const findCommonalities = (id) => {
       |                              ^^
    24 |     const person = employeesData.find((e) => e.id === parseInt(id));
    25 |     if (!person) return;
    26 |

ERROR in ./src/CompareEmployees.tsx:40:22
TS2345: Argument of type '{ name: string; shared: string[]; }[]' is not assignable to parameter of type 'SetStateAction<never[]>'.
  Type '{ name: string; shared: string[]; }[]' is not assignable to type 'never[]'.
    Type '{ name: string; shared: string[]; }' is not assignable to type 'never'.
    38 |       .filter((entry) => entry.shared.length > 0);
    39 |
  > 40 |     setCommonalities(results);
       |                      ^^^^^^^
    41 |   };
    42 |
    43 |   return (

ERROR in ./src/CompareEmployees.tsx:47:8
TS2304: Cannot find name 'Card'.
    45 |       <h1 className="text-2xl font-bold text-[#003F5F]">JPMorgan Chase Employee Dashboard</h1>
    46 |
  > 47 |       <Card>
       |        ^^^^
    48 |         <CardContent className="p-4">
    49 |           <h2 className="text-xl font-semibold mb-2">Top RSVPed Events</h2>
    50 |           <ResponsiveContainer width="100%" height={300}>

ERROR in ./src/CompareEmployees.tsx:48:10
TS2304: Cannot find name 'CardContent'.
    46 |
    47 |       <Card>
  > 48 |         <CardContent className="p-4">
       |          ^^^^^^^^^^^
    49 |           <h2 className="text-xl font-semibold mb-2">Top RSVPed Events</h2>
    50 |           <ResponsiveContainer width="100%" height={300}>
    51 |             <BarChart data={topEvents}>

ERROR in ./src/CompareEmployees.tsx:58:11
TS2304: Cannot find name 'CardContent'.
    56 |             </BarChart>
    57 |           </ResponsiveContainer>
  > 58 |         </CardContent>
       |           ^^^^^^^^^^^
    59 |       </Card>
    60 |
    61 |       <Card>

ERROR in ./src/CompareEmployees.tsx:59:9
TS2304: Cannot find name 'Card'.
    57 |           </ResponsiveContainer>
    58 |         </CardContent>
  > 59 |       </Card>
       |         ^^^^
    60 |
    61 |       <Card>
    62 |         <CardContent className="p-4">

ERROR in ./src/CompareEmployees.tsx:61:8
TS2304: Cannot find name 'Card'.
    59 |       </Card>
    60 |
  > 61 |       <Card>
       |        ^^^^
    62 |         <CardContent className="p-4">
    63 |           <h2 className="text-xl font-semibold mb-2">Find Commonalities</h2>
    64 |           <select

ERROR in ./src/CompareEmployees.tsx:62:10
TS2304: Cannot find name 'CardContent'.
    60 |
    61 |       <Card>
  > 62 |         <CardContent className="p-4">
       |          ^^^^^^^^^^^
    63 |           <h2 className="text-xl font-semibold mb-2">Find Commonalities</h2>
    64 |           <select
    65 |             className="border p-2 rounded w-full mb-4"

ERROR in ./src/CompareEmployees.tsx:84:30
TS2339: Property 'name' does not exist on type 'never'.
    82 |               {commonalities.map((c, index) => (
    83 |                 <li key={index}>
  > 84 |                   <strong>{c.name}:</strong> {c.shared.join(', ')}
       |                              ^^^^
    85 |                 </li>
    86 |               ))}
    87 |             </ul>

ERROR in ./src/CompareEmployees.tsx:84:49
TS2339: Property 'shared' does not exist on type 'never'.
    82 |               {commonalities.map((c, index) => (
    83 |                 <li key={index}>
  > 84 |                   <strong>{c.name}:</strong> {c.shared.join(', ')}
       |                                                 ^^^^^^
    85 |                 </li>
    86 |               ))}
    87 |             </ul>

ERROR in ./src/CompareEmployees.tsx:89:11
TS2304: Cannot find name 'CardContent'.
    87 |             </ul>
    88 |           )}
  > 89 |         </CardContent>
       |           ^^^^^^^^^^^
    90 |       </Card>
    91 |     </div>
    92 |   );

ERROR in ./src/CompareEmployees.tsx:90:9
TS2304: Cannot find name 'Card'.
    88 |           )}
    89 |         </CardContent>
  > 90 |       </Card>
       |         ^^^^
    91 |     </div>
    92 |   );
    93 | }

Found 14 errors in 13997 ms.

