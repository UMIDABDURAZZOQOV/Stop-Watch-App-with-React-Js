# Stop-Watch-App-with-React-Js

⏱️ React Stopwatch
A sleek, high-precision stopwatch application built with React.js. This project demonstrates the effective use of React Hooks like useState, useEffect, and useRef to handle real-time UI updates and DOM-independent timing logic.

✨ Features
Precision Timing: Tracks time down to the centisecond (10ms intervals).

Persistent Logic: Uses Date.now() to ensure timing remains accurate even if the browser's main thread is busy.

Functionality:

Start: Commences the timer or resumes from a paused state.

Stop: Freezes the timer at the current elapsed time.

Reset: Clears all data and returns the display to 00:00:00.

Clean UI: Minimalist and responsive design.

🚀 Technologies Used
React.js (Functional Components)

JavaScript (ES6+)

CSS3 (Custom Styling & Flexbox)


🧠 Technical Highlights
This project was a deep dive into React's lifecycle and state management:

useRef: Utilized to store the intervalId and the startTime without triggering unnecessary re-renders. This ensures that the timer logic stays decoupled from the UI rendering.

useEffect: Handles the side effect of starting and clearing the setInterval based on the isRunning state. Includes a cleanup function to prevent memory leaks.

useState: Manages the dynamic data displayed on the screen, such as the elapsed time and the active status of the stopwatch.

📝 License
Distributed under the MIT License. See LICENSE for more information.

Stopwatch.jsx

```
import React, {useState, useEffect, useRef} from 'react'


function Stopwatch(){


    const [isRunning, setIsRunning] = useState(false)
    const [elapsedTime, setElapsedTime] = useState(0)
    const intervalIdRef = useRef(null)
    const startTimeRef = useRef(0);

    useEffect(() => {
    let intervalId;

    if(isRunning){
        intervalId = setInterval(() => {
            setElapsedTime(Date.now() - startTimeRef.current)
        }, 10)

        intervalIdRef.current = intervalId;
    }

    return () => {
        clearInterval(intervalIdRef.current)
    }

    }, [isRunning])

    function start(){
        setIsRunning(true)
        startTimeRef.current = Date.now() - elapsedTime
    }
    function end(){
        setIsRunning(false);

    }
    function reset(){
        setElapsedTime(0)
        setIsRunning(false)
    }

    function formatTime(){
        let hours = Math.floor(elapsedTime / (1000 * 60 * 60))
         let minutes = Math.floor(elapsedTime / (1000 * 60) % 60)
             let seconds = Math.floor(elapsedTime / (1000) % 60)
                 let milliseconds = Math.floor((elapsedTime % 1000) / 10)
        
                 hours = String(hours).padStart(2, "0")
                  minutes = String(minutes).padStart(2, "0")
                   seconds = String(seconds).padStart(2, "0")
                     milliseconds = String(milliseconds).padStart(2, "0")
                

        return `${minutes}:${seconds}:${milliseconds}`
    }

    return(<div className='stopwatch'>
    
     <div className='display'>{formatTime()}</div>
        <div className='controls'>
            <button onClick={start} className='start-button'>Start</button>
            <button onClick={end} className='stop-button'>Stop</button>
            <button onClick={reset} className='reset-button'>Reset</button>
        </div>
    </div>)
}
export default Stopwatch

```

index.css

```
body{
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: white
}

.stopwatch{
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 5px solid;
    border-radius: 50px;
    background-color: white;
    padding: 30px;
}
.display{
    font-size: 5rem;
    font-family: monospace;
    font-weight: bold;
    color: hsl(0, 0%, 49%);
    text-shadow: 2px 2px 2px hsl(0, 0%, 3%);
    margin-bottom: 25px;
}

.controls button{
    font-size: 1.5rem;
    font-weight: bold;
    padding: 10px 20px;
    margin: 5px;
    min-width: 125px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    color: white;
    transition: background-color 0.5s ease;
}
.start-button{
    background-color: hsl(120, 100%, 42%);

}
.start-button:hover{
    background-color: hsl(120, 93%, 32%);
    
}

.stop-button{
    background-color: hsl(0, 96%, 48%);

}
.stop-button:hover{
    background-color: hsl(0, 91%, 38%);
    
}

.reset-button{
    background-color: hsl(241, 100%, 50%);

}
.reset-button:hover{
    background-color: hsl(241, 86%, 34%);
    
}

```

main.jsx

```
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(

    <App />
 
)

```



App.jsx

```
import Stopwatch from "./Stopwatch"

function App() {
  return (
    <>
        <Stopwatch/>
    </>
  )
}

export default App

```

<img width="671" height="263" alt="StopWatchAPP" src="https://github.com/user-attachments/assets/b609e861-0e5e-4da3-8959-ca2ce49a1568" />

