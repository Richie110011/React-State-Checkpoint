import React, { Component } from "react";
import "./App.css";

class App extends Component {
  constructor(props) {
    super(props);

    // Initialize state
    this.state = {
      person: {
        fullName: "John Doe",
        bio: "A passionate developer who loves React!",
        imgSrc: "https://via.placeholder.com/150",
        profession: "Software Engineer"
      },
      shows: false,
      timeSinceMount: 0
    };
  }

  // Toggle show/hide profile
  toggleProfile = () => {
    this.setState({ shows: !this.state.shows });
  };

  // Lifecycle method: runs after component is mounted
  componentDidMount() {
    // Start timer to update timeSinceMount every second
    this.interval = setInterval(() => {
      this.setState(prevState => ({
        timeSinceMount: prevState.timeSinceMount + 1
      }));
    }, 1000);
  }

  // Clear interval when component unmounts
  componentWillUnmount() {
    clearInterval(this.interval);
  }

  render() {
    const { fullName, bio, imgSrc, profession } = this.state.person;

    return (
      <div className="App" style={{ textAlign: "center", marginTop: "2rem" }}>
        <button onClick={this.toggleProfile} style={{ padding: "10px 20px", fontSize: "16px" }}>
          {this.state.shows ? "Hide Profile" : "Show Profile"}
        </button>

        {this.state.shows && (
          <div style={{ marginTop: "2rem", display: "inline-block", textAlign: "left", border: "1px solid #ccc", borderRadius: "10px", padding: "20px", width: "300px" }}>
            <img src={imgSrc} alt={fullName} style={{ width: "100%", borderRadius: "10px" }} />
            <h2>{fullName}</h2>
            <p><strong>Bio:</strong> {bio}</p>
            <p><strong>Profession:</strong> {profession}</p>
          </div>
        )}

        <div style={{ marginTop: "20px", fontStyle: "italic" }}>
          Time since component mounted: {this.state.timeSinceMount} second{this.state.timeSinceMount !== 1 ? "s" : ""}
        </div>
      </div>
    );
  }
}

export default App;
