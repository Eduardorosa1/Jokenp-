import { useState } from "react";

import "./styles.css";

export default function App() {
  const [pc, setpc] = useState("");
  const [foto, setfoto] = useState("");
  const [venceu, setvenceu] = useState(0);
  const [perdeu, setperdeu] = useState(0);
  const [empate, setempate] = useState(0);
  const [status, setstatus] = useState("Jogo Iniciado");

  function reiniciar() {
    setfoto("");
    setpc("");
    setstatus("Jogo Reiniciado");
  }

  function papel() {
    setfoto("papel.png");
  }
  function pedra() {
    setfoto("pedra.png");
  }
  function tesoura() {
    setfoto("tesoura.png");
  }

  function escpc() {
    if (foto === "") {
      alert("Escolha uma Mão");
      return;
    }
    if (pc !== "") {
      alert("Escolha uma Nova Mão");
      return;
    }
    var rnd = Math.ceil(Math.random() * 3);
    let verificar;
    if (rnd === 1) {
      verificar = "papel.png";
    } else if (rnd === 2) {
      verificar = "pedra.png";
    } else {
      verificar = "tesoura.png";
    }
    setpc(verificar);

    if (foto === "papel.png") {
      if (verificar === "papel.png") {
        setempate(empate + 1);
        setstatus("Empate");
      } else if (verificar === "tesoura.png") {
        setperdeu(perdeu + 1);
        setstatus("Perdeu!");
      } else {
        setperdeu(perdeu + 1);
        setstatus("Perdeu!");
      }
    }
    if (foto === "pedra.png") {
      if (verificar === "pedra.png") {
        setempate(empate + 1);
        setstatus("Empate!");
      } else if (verificar === "tesoura.png") {
        setvenceu(venceu + 1);
        setstatus("Venceu!");
      } else {
        setperdeu(perdeu + 1);
        setstatus("perdeu!");
      }
    }
    if (foto === "tesoura.png") {
      if (verificar === "tesoura.png") {
        setempate(empate + 1);
        setstatus("Empate!");
      } else if (verificar === "pedra.png") {
        setperdeu(perdeu + 1);
        setstatus("Perdeu!");
      } else {
        setvenceu(venceu + 1);
        setstatus("Venceu!");
      }
    }
  }

  return (
    <>
      <div className="App">
        <h1>Jogo Pedra Papel e Tesoura</h1>
        <h2>Clique sobre a imagem:</h2>
        <img src="papel.png" className="pedra" onClick={papel} />
        <img src="pedra.png" className="pedra" onClick={pedra} />
        <img src="tesoura.png" className="tesoura" onClick={tesoura} />
        <h3>Sua aposta</h3>
        {foto && <img src={foto} alt="Escolha do jogador" />}
        <br />
        <br />
        <h4> X </h4>
        {pc && <img src={pc} alt="Escolha do verificar" />}
      </div>
      <br />
      <br />
      <br />
      <br />
      <div className="d-flex justify-content-center">
        <button class="btn btn-success ms-1" onClick={escpc}>
          Desafiar PC
        </button>
      </div>
      <br />
      <br />
      <div>
        <p className="d-flex justify-content-center">
          Mesagem: <spam className="text text-success">{status}</spam>
        </p>
      </div>
      <div>
        <p className="d-flex justify-content-center">
          Numero de Empates: <span className="text text-primary">{empate}</span>
        </p>
      </div>
      <div>
        <p className="d-flex justify-content-center">
          Ganhas por Humano: <span className="text text-success">{venceu}</span>
        </p>
      </div>
      <div>
        <p className="d-flex justify-content-center">
          Ganhas por Maquina: <span className="text text-danger">{perdeu}</span>
        </p>
      </div>
      <br />
      <div className="d-flex justify-content-center">
        <button class="btn btn-primary ms-1" onClick={reiniciar}>
          Reiniciar Jogo!
        </button>
      </div>
    </>
  );
}
