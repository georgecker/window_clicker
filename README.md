# Window_clicker
A rhythm driven game, where you have to close windows 95 error pop-ups on time to prevent your shitbox from getting infected.

## TODOs
* STATE 1:
  * Clickable window template -> HTML component
  * Windows background
  * Make music playable on webpage
  * Extract beats from music file
  * Map window closing click to beat
    * Add error margin maybe 0.3 - 1.0 sec
    * Send Json from backend to frontend
  * Game loop
    * Loose life on failed window -> Plant easter egg
    * Sunshine if u win

## Tech 
Backend => Atix
Frontend => TODO
DB => SQLite probaly

## Build:
Currently you have to build and run the server and the client separately

### Client:
```
# Start in the window_clicker dir 
cd server 

# Install node modules if not done so bevore
bun install 

# Run client in dev mode
bun run dev
```

### Server:
```
cargo run
```

* Might add cargo-make in the future, depending on the size of the project. Or if it just annoys me to build the server and client separately
