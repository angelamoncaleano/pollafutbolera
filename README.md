import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Table, TableHeader, TableRow, TableHead, TableBody, TableCell } from "@/components/ui/table";

export default function PollaVirtual() {
  const [predictions, setPredictions] = useState([]);
  const [name, setName] = useState("");
  const [team, setTeam] = useState("");

  const handleSubmit = () => {
    if (name && team) {
      setPredictions([...predictions, { name, team, score: Math.floor(Math.random() * 100) }]);
      setName("");
      setTeam("");
    }
  };

  return (
    <div className="p-6 space-y-6">
      <h1 className="text-xl font-bold">Polla Virtual - Predicciones</h1>
      
      <Card>
        <CardContent className="p-4 space-y-4">
          <Input placeholder="Tu nombre" value={name} onChange={(e) => setName(e.target.value)} />
          <Input placeholder="Equipo ganador" value={team} onChange={(e) => setTeam(e.target.value)} />
          <Button onClick={handleSubmit}>Enviar Predicción</Button>
        </CardContent>
      </Card>
      
      <h2 className="text-lg font-semibold">Ranking de Participantes</h2>
      <Table>
        <TableHeader>
          <TableRow>
            <TableHead>Nombre</TableHead>
            <TableHead>Equipo</TableHead>
            <TableHead>Puntaje</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          {predictions.sort((a, b) => b.score - a.score).map((entry, index) => (
            <TableRow key={index}>
              <TableCell>{entry.name}</TableCell>
              <TableCell>{entry.team}</TableCell>
              <TableCell>{entry.score}</TableCell>
            </TableRow>
          ))}
        </TableBody>
      </Table>
    </div>
  );
}

