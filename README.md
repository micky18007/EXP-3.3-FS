import React, { useState } from "react";

export default function PersonApp() {
  const [people, setPeople] = useState([
    { id: 1, type: "Student", name: "Aman", age: 20, grade: "A" },
    { id: 2, type: "Teacher", name: "Riya", age: 35, subject: "Math" },
  ]);
  const [search, setSearch] = useState("");

  const filtered = people.filter((p) =>
    p.name.toLowerCase().includes(search.toLowerCase())
  );

  const removePerson = (id) => {
    setPeople(people.filter((p) => p.id !== id));
  };

  return (
    <div
      className="min-h-screen p-6 flex flex-col items-center"
      style={{
        background: "linear-gradient(135deg, #87CEFA, #00BFFF, #E0FFFF)",
      }}
    >
      <h1
        style={{
          fontFamily: "Arial, sans-serif",
          fontSize: "3rem",
          color: "#fff",
          textShadow: "2px 2px 8px rgba(0,0,0,0.3)",
          marginBottom: "2rem",
        }}
      >
        Person Hierarchy
      </h1>

      <input
        type="text"
        placeholder="Search person..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        style={{
          padding: "0.5rem 1rem",
          borderRadius: "1rem",
          border: "none",
          width: "20rem",
          marginBottom: "2rem",
          backdropFilter: "blur(10px)",
          background: "rgba(255,255,255,0.3)",
          color: "#000",
          fontSize: "1rem",
        }}
      />

      <div style={{ display: "flex", gap: "2rem", flexWrap: "wrap" }}>
        {filtered.map((p) => (
          <div
            key={p.id}
            style={{
              padding: "1.5rem",
              borderRadius: "1.5rem",
              minWidth: "15rem",
              backdropFilter: "blur(15px)",
              background: "rgba(255,255,255,0.2)",
              boxShadow: "0 8px 20px rgba(0,0,0,0.25)",
              color: "#fff",
              display: "flex",
              flexDirection: "column",
              gap: "0.5rem",
              transition: "transform 0.3s, box-shadow 0.3s",
            }}
            onMouseEnter={(e) => {
              e.currentTarget.style.transform = "scale(1.05)";
              e.currentTarget.style.boxShadow = "0 12px 30px rgba(0,0,0,0.35)";
            }}
            onMouseLeave={(e) => {
              e.currentTarget.style.transform = "scale(1)";
              e.currentTarget.style.boxShadow = "0 8px 20px rgba(0,0,0,0.25)";
            }}
          >
            <h2 style={{ fontSize: "1.5rem", fontWeight: "bold" }}>{p.name}</h2>
            <p>{p.type}</p>
            <p>Age: {p.age}</p>
            {p.type === "Student" && <p>Grade: {p.grade}</p>}
            {p.type === "Teacher" && <p>Subject: {p.subject}</p>}
            <button
              onClick={() => removePerson(p.id)}
              style={{
                marginTop: "1rem",
                padding: "0.5rem 1rem",
                borderRadius: "1rem",
                border: "none",
                cursor: "pointer",
                background:
                  "linear-gradient(90deg, #00BFFF, #87CEFA, #1E90FF)",
                color: "#fff",
                fontWeight: "bold",
                transition: "transform 0.2s, box-shadow 0.2s",
              }}
              onMouseEnter={(e) => {
                e.currentTarget.style.transform = "scale(1.1)";
                e.currentTarget.style.boxShadow = "0 4px 12px rgba(0,0,0,0.3)";
              }}
              onMouseLeave={(e) => {
                e.currentTarget.style.transform = "scale(1)";
                e.currentTarget.style.boxShadow = "none";
              }}
            >
              Remove
            </button>
          </div>
        ))}
      </div>

      <div style={{ marginTop: "2rem", display: "flex", gap: "1rem" }}>
        <button
          onClick={() =>
            setPeople([
              ...people,
              { id: Date.now(), type: "Student", name: "New Student", age: 18, grade: "B" },
            ])
          }
          style={{
            padding: "0.5rem 1rem",
            borderRadius: "1rem",
            border: "none",
            cursor: "pointer",
            background: "linear-gradient(90deg, #87CEFA, #00BFFF)",
            color: "#fff",
            fontWeight: "bold",
          }}
        >
          ➕ Add Student
        </button>

        <button
          onClick={() =>
            setPeople([
              ...people,
              { id: Date.now(), type: "Teacher", name: "New Teacher", age: 30, subject: "Science" },
            ])
          }
          style={{
            padding: "0.5rem 1rem",
            borderRadius: "1rem",
            border: "none",
            cursor: "pointer",
            background: "linear-gradient(90deg, #1E90FF, #00BFFF)",
            color: "#fff",
            fontWeight: "bold",
          }}
        >
          ➕ Add Teacher
        </button>
      </div>
    </div>
  );
}
