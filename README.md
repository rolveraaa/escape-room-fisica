<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Escape Room - Laboratorio de Mecánica</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        const EscapeRoomFisica = () => {
          const [currentRoom, setCurrentRoom] = useState('inicio');
          const [inventory, setInventory] = useState([]);
          const [answers, setAnswers] = useState({});
          const [briefcaseCode, setBriefcaseCode] = useState(['', '', '', '']);

          const addToInventory = (item) => {
            if (!inventory.includes(item)) {
              setInventory([...inventory, item]);
            }
          };

          const handleAnswer = (puzzle, answer, correctAnswer, reward) => {
            if (answer.toLowerCase().trim() === correctAnswer.toLowerCase()) {
              setAnswers({...answers, [puzzle]: true});
              addToInventory(reward);
              return true;
            }
            return false;
          };

          const checkBriefcase = () => {
            const correctCode = ['3', '5', '2', '1'];
            return briefcaseCode.join('') === correctCode.join('');
          };

          // Pantalla de inicio
          if (currentRoom === 'inicio') {
            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-blue-900 to-slate-900 flex items-center justify-center p-4">
                <div className="max-w-2xl w-full bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8 border border-blue-500/30">
                  <div className="text-center mb-8">
                    <div className="text-7xl mb-4">🧮</div>
                    <h1 className="text-4xl font-bold text-white mb-4">
                      Laboratorio de Mecánica
                    </h1>
                    <div className="h-1 w-32 bg-blue-500 mx-auto mb-6"></div>
                  </div>
                  
                  <div className="bg-slate-700/50 rounded-lg p-6 mb-6 border border-slate-600">
                    <h2 className="text-2xl font-bold text-blue-300 mb-4">Tu Misión:</h2>
                    <p className="text-slate-200 text-lg leading-relaxed mb-4">
                      Eres un <strong className="text-blue-400">físico novato</strong> que aspira a convertirse en todo un <strong className="text-blue-400">experto en Mecánica</strong>.
                    </p>
                    <p className="text-slate-200 text-lg leading-relaxed mb-4">
                      Para conseguirlo, debes adentrarte en los <strong className="text-yellow-400">desafíos del laboratorio</strong> y resolver los problemas que encontrarás.
                    </p>
                    <p className="text-slate-200 text-lg leading-relaxed mb-4">
                      Asegúrate de anotar las <strong className="text-green-400">ecuaciones y datos</strong> que irás obteniendo en tu cuaderno.
                    </p>
                    <p className="text-slate-200 text-lg leading-relaxed">
                      Si resuelves todos los problemas correctamente, obtendrás la <strong className="text-purple-400">fórmula maestra</strong> que abre el maletín con tu recompensa.
                    </p>
                  </div>

                  <button
                    onClick={() => setCurrentRoom('mapa')}
                    className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 px-6 rounded-lg transition-all transform hover:scale-105 flex items-center justify-center gap-3"
                  >
                    Comenzar Aventura ➜
                  </button>
                </div>
              </div>
            );
          }

          // Pantalla del mapa
          if (currentRoom === 'mapa') {
            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 p-4">
                <div className="max-w-6xl mx-auto">
                  <div className="bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-6 mb-4">
                    <h1 className="text-3xl font-bold text-white mb-4 flex items-center gap-3">
                      📚 Mapa del Laboratorio
                    </h1>
                    <div className="bg-slate-700/50 rounded-lg p-4">
                      <h3 className="text-lg font-semibold text-purple-300 mb-2">Tu Cuaderno de Apuntes:</h3>
                      <div className="flex flex-wrap gap-2">
                        {inventory.length === 0 ? (
                          <p className="text-slate-400">Aún no has recolectado ninguna pista...</p>
                        ) : (
                          inventory.map((item, idx) => (
                            <span key={idx} className="bg-purple-600 text-white px-3 py-1 rounded-full text-sm">
                              {item}
                            </span>
                          ))
                        )}
                      </div>
                    </div>
                  </div>

                  <div className="grid md:grid-cols-2 gap-4 mb-4">
                    <button
                      onClick={() => setCurrentRoom('sala1')}
                      className="bg-gradient-to-br from-blue-600 to-blue-800 hover:from-blue-700 hover:to-blue-900 text-white p-6 rounded-xl transition-all transform hover:scale-105 shadow-lg"
                    >
                      <div className="text-6xl mb-3">🔬</div>
                      <h2 className="text-2xl font-bold mb-2">Sala de Colisiones</h2>
                      <p className="text-blue-100">Resuelve el problema de la granada</p>
                      {answers.sala1 && <div className="mt-2 text-green-300">✓ Completado</div>}
                    </button>

                    <button
                      onClick={() => setCurrentRoom('sala2')}
                      className="bg-gradient-to-br from-green-600 to-green-800 hover:from-green-700 hover:to-green-900 text-white p-6 rounded-xl transition-all transform hover:scale-105 shadow-lg"
                    >
                      <div className="text-6xl mb-3">⚙️</div>
                      <h2 className="text-2xl font-bold mb-2">Sala de Rotación</h2>
                      <p className="text-green-100">Calcula la velocidad angular</p>
                      {answers.sala2 && <div className="mt-2 text-green-300">✓ Completado</div>}
                    </button>

                    <button
                      onClick={() => setCurrentRoom('sala3')}
                      className="bg-gradient-to-br from-yellow-600 to-yellow-800 hover:from-yellow-700 hover:to-yellow-900 text-white p-6 rounded-xl transition-all transform hover:scale-105 shadow-lg"
                    >
                      <div className="text-6xl mb-3">🎯</div>
                      <h2 className="text-2xl font-bold mb-2">Sala de Energía</h2>
                      <p className="text-yellow-100">Analiza el péndulo</p>
                      {answers.sala3 && <div className="mt-2 text-green-300">✓ Completado</div>}
                    </button>

                    <button
                      onClick={() => setCurrentRoom('maletin')}
                      className="bg-gradient-to-br from-purple-600 to-purple-800 hover:from-purple-700 hover:to-purple-900 text-white p-6 rounded-xl transition-all transform hover:scale-105 shadow-lg"
                    >
                      <div className="text-6xl mb-3">💼</div>
                      <h2 className="text-2xl font-bold mb-2">Maletín Final</h2>
                      <p className="text-purple-100">Introduce el código</p>
                      <p className="text-sm text-purple-200 mt-1">Necesitas todas las pistas</p>
                    </button>
                  </div>

                  <button
                    onClick={() => setCurrentRoom('inicio')}
                    className="bg-slate-700 hover:bg-slate-600 text-white px-6 py-3 rounded-lg flex items-center gap-2 mx-auto"
                  >
                    ↺ Volver al Inicio
                  </button>
                </div>
              </div>
            );
          }

          // Sala 1: Granada
          if (currentRoom === 'sala1') {
            const [input, setInput] = useState('');
            const [feedback, setFeedback] = useState('');

            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-blue-900 to-slate-900 p-4">
                <div className="max-w-3xl mx-auto">
                  <div className="bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8">
                    <h2 className="text-3xl font-bold text-white mb-6">🔬 Sala de Colisiones</h2>
                    
                    <div className="bg-blue-900/30 rounded-lg p-6 mb-6 border border-blue-500/30">
                      <h3 className="text-xl font-bold text-blue-300 mb-4">Problema:</h3>
                      <p className="text-slate-200 mb-4">
                        Una granada explota en tres fragmentos. El fragmento 2 tiene una masa m₂ = m₀/3 y un momento lineal p₂ = p₀/2.
                      </p>
                      <p className="text-slate-200 mb-4">
                        <strong className="text-yellow-300">Pregunta:</strong> ¿Cuántas veces v₀ es la velocidad del fragmento 2?
                      </p>
                      <p className="text-slate-300 text-sm">
                        💡 Pista: Usa la fórmula p = mv, donde p es momento, m es masa y v es velocidad.
                      </p>
                    </div>

                    <div className="mb-6">
                      <label className="block text-white mb-2 font-semibold">Tu respuesta (solo el número):</label>
                      <input
                        type="text"
                        value={input}
                        onChange={(e) => setInput(e.target.value)}
                        className="w-full p-3 rounded-lg bg-slate-700 text-white border border-slate-600 focus:border-blue-500 focus:outline-none"
                        placeholder="Ejemplo: 1.5"
                      />
                    </div>

                    {feedback && (
                      <div className={`p-4 rounded-lg mb-4 ${feedback.includes('Correcto') ? 'bg-green-600' : 'bg-red-600'}`}>
                        <p className="text-white font-semibold">{feedback}</p>
                      </div>
                    )}

                    <div className="flex gap-4">
                      <button
                        onClick={() => {
                          if (handleAnswer('sala1', input, '1.5', 'Dígito #1: 3')) {
                            setFeedback('¡Correcto! Has obtenido el primer dígito: 3');
                          } else {
                            setFeedback('Incorrecto. Recuerda: v = p/m. Calcula v₂ = (p₀/2)/(m₀/3)');
                          }
                        }}
                        className="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg transition-all"
                      >
                        Verificar Respuesta
                      </button>
                      <button
                        onClick={() => setCurrentRoom('mapa')}
                        className="bg-slate-700 hover:bg-slate-600 text-white px-6 py-3 rounded-lg"
                      >
                        Volver al Mapa
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            );
          }

          // Sala 2: Rotación
          if (currentRoom === 'sala2') {
            const [input, setInput] = useState('');
            const [feedback, setFeedback] = useState('');

            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-green-900 to-slate-900 p-4">
                <div className="max-w-3xl mx-auto">
                  <div className="bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8">
                    <h2 className="text-3xl font-bold text-white mb-6">⚙️ Sala de Rotación</h2>
                    
                    <div className="bg-green-900/30 rounded-lg p-6 mb-6 border border-green-500/30">
                      <h3 className="text-xl font-bold text-green-300 mb-4">Problema:</h3>
                      <p className="text-slate-200 mb-4">
                        Un disco gira con velocidad angular constante. Si completa 10 vueltas en 4 segundos...
                      </p>
                      <p className="text-slate-200 mb-4">
                        <strong className="text-yellow-300">Pregunta:</strong> ¿Cuál es su velocidad angular en rad/s? (Redondea al entero más cercano)
                      </p>
                      <p className="text-slate-300 text-sm">
                        💡 Pista: Una vuelta completa = 2π radianes. ω = θ/t
                      </p>
                    </div>

                    <div className="mb-6">
                      <label className="block text-white mb-2 font-semibold">Tu respuesta (rad/s):</label>
                      <input
                        type="text"
                        value={input}
                        onChange={(e) => setInput(e.target.value)}
                        className="w-full p-3 rounded-lg bg-slate-700 text-white border border-slate-600 focus:border-green-500 focus:outline-none"
                        placeholder="Ejemplo: 15"
                      />
                    </div>

                    {feedback && (
                      <div className={`p-4 rounded-lg mb-4 ${feedback.includes('Correcto') ? 'bg-green-600' : 'bg-red-600'}`}>
                        <p className="text-white font-semibold">{feedback}</p>
                      </div>
                    )}

                    <div className="flex gap-4">
                      <button
                        onClick={() => {
                          if (handleAnswer('sala2', input, '5', 'Dígito #2: 5')) {
                            setFeedback('¡Correcto! Has obtenido el segundo dígito: 5');
                          } else {
                            setFeedback('Incorrecto. Piensa: 10 vueltas en 4 segundos = 2.5 vueltas por segundo. El dígito que buscas es 5');
                          }
                        }}
                        className="flex-1 bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-6 rounded-lg transition-all"
                      >
                        Verificar Respuesta
                      </button>
                      <button
                        onClick={() => setCurrentRoom('mapa')}
                        className="bg-slate-700 hover:bg-slate-600 text-white px-6 py-3 rounded-lg"
                      >
                        Volver al Mapa
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            );
          }

          // Sala 3: Péndulo
          if (currentRoom === 'sala3') {
            const [input, setInput] = useState('');
            const [feedback, setFeedback] = useState('');

            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-yellow-900 to-slate-900 p-4">
                <div className="max-w-3xl mx-auto">
                  <div className="bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8">
                    <h2 className="text-3xl font-bold text-white mb-6">🎯 Sala de Energía</h2>
                    
                    <div className="bg-yellow-900/30 rounded-lg p-6 mb-6 border border-yellow-500/30">
                      <h3 className="text-xl font-bold text-yellow-300 mb-4">Problema:</h3>
                      <p className="text-slate-200 mb-4">
                        Una masa cae desde una altura de 20 metros. Considerando g = 10 m/s².
                      </p>
                      <p className="text-slate-200 mb-4">
                        <strong className="text-yellow-300">Pregunta:</strong> ¿Cuántos segundos tarda en llegar al suelo?
                      </p>
                      <p className="text-slate-300 text-sm">
                        💡 Pista: Usa h = ½gt². Despeja t.
                      </p>
                    </div>

                    <div className="mb-6">
                      <label className="block text-white mb-2 font-semibold">Tu respuesta (segundos):</label>
                      <input
                        type="text"
                        value={input}
                        onChange={(e) => setInput(e.target.value)}
                        className="w-full p-3 rounded-lg bg-slate-700 text-white border border-slate-600 focus:border-yellow-500 focus:outline-none"
                        placeholder="Ejemplo: 3"
                      />
                    </div>

                    {feedback && (
                      <div className={`p-4 rounded-lg mb-4 ${feedback.includes('Correcto') ? 'bg-green-600' : 'bg-red-600'}`}>
                        <p className="text-white font-semibold">{feedback}</p>
                      </div>
                    )}

                    <div className="flex gap-4">
                      <button
                        onClick={() => {
                          if (handleAnswer('sala3', input, '2', 'Dígito #3: 2')) {
                            setFeedback('¡Correcto! Has obtenido el tercer dígito: 2');
                          } else {
                            setFeedback('Incorrecto. De h = ½gt², despeja t = √(2h/g) = √(40/10) = √4 = 2');
                          }
                        }}
                        className="flex-1 bg-yellow-600 hover:bg-yellow-700 text-white font-bold py-3 px-6 rounded-lg transition-all"
                      >
                        Verificar Respuesta
                      </button>
                      <button
                        onClick={() => setCurrentRoom('mapa')}
                        className="bg-slate-700 hover:bg-slate-600 text-white px-6 py-3 rounded-lg"
                      >
                        Volver al Mapa
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            );
          }

          // Maletín Final
          if (currentRoom === 'maletin') {
            const [feedback, setFeedback] = useState('');

            return (
              <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 p-4">
                <div className="max-w-3xl mx-auto">
                  <div className="bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8">
                    <h2 className="text-3xl font-bold text-white mb-6 flex items-center gap-3">
                      🔒 Maletín Final
                    </h2>
                    
                    <div className="bg-purple-900/30 rounded-lg p-6 mb-6 border border-purple-500/30">
                      <h3 className="text-xl font-bold text-purple-300 mb-4">¡Última Prueba!</h3>
                      <p className="text-slate-200 mb-4">
                        Has recolectado {inventory.length} de 3 pistas necesarias.
                      </p>
                      <div className="bg-slate-700/50 rounded-lg p-4 mb-4">
                        {inventory.map((item, idx) => (
                          <div key={idx} className="text-green-300 mb-2">✓ {item}</div>
                        ))}
                      </div>
                      {inventory.length < 3 ? (
                        <p className="text-yellow-300">
                          ⚠️ Necesitas resolver todos los problemas para obtener el código completo.
                        </p>
                      ) : (
                        <div>
                          <p className="text-slate-200 mb-4">
                            Introduce el código de 4 dígitos en orden. El último dígito es <strong className="text-green-400">1</strong>.
                          </p>
                          <p className="text-slate-300 text-sm">
                            💡 Pista: Ordena los dígitos que obtuviste: primer problema, segundo problema, tercer problema, y agrega el 1 al final.
                          </p>
                        </div>
                      )}
                    </div>

                    <div className="mb-6">
                      <label className="block text-white mb-4 font-semibold text-center">Código del Maletín:</label>
                      <div className="flex gap-4 justify-center mb-6">
                        {[0, 1, 2, 3].map((idx) => (
                          <input
                            key={idx}
                            type="text"
                            maxLength="1"
                            value={briefcaseCode[idx]}
                            onChange={(e) => {
                              const newCode = [...briefcaseCode];
                              newCode[idx] = e.target.value;
                              setBriefcaseCode(newCode);
                            }}
                            className="w-16 h-16 text-center text-3xl font-bold rounded-lg bg-slate-700 text-white border-2 border-purple-500 focus:border-purple-300 focus:outline-none"
                            disabled={inventory.length < 3}
                          />
                        ))}
                      </div>
                    </div>

                    {feedback && (
                      <div className={`p-4 rounded-lg mb-4 text-center ${feedback.includes('¡FELICIDADES') ? 'bg-green-600' : 'bg-red-600'}`}>
                        <p className="text-white font-bold text-lg">{feedback}</p>
                      </div>
                    )}

                    <div className="flex gap-4">
                      <button
                        onClick={() => {
                          if (checkBriefcase()) {
                            setFeedback('¡FELICIDADES! 🎉 Has completado el Escape Room. ¡Eres ahora un experto en Mecánica!');
                            setCurrentRoom('victoria');
                          } else {
                            setFeedback('Código incorrecto. Revisa tus pistas y el orden de los dígitos.');
                          }
                        }}
                        className="flex-1 bg-purple-600 hover:bg-purple-700 text-white font-bold py-3 px-6 rounded-lg transition-all disabled:opacity-50 disabled:cursor-not-allowed"
                        disabled={inventory.length < 3}
                      >
                        Abrir Maletín
                      </button>
                      <button
                        onClick={() => setCurrentRoom('mapa')}
                        className="bg-slate-700 hover:bg-slate-600 text-white px-6 py-3 rounded-lg"
                      >
                        Volver al Mapa
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            );
          }

          // Pantalla de Victoria
          if (currentRoom === 'victoria') {
            return (
              <div className="min-h-screen bg-gradient-to-br from-green-900 via-emerald-800 to-green-900 flex items-center justify-center p-4">
                <div className="max-w-2xl w-full bg-slate-800/90 backdrop-blur rounded-2xl shadow-2xl p-8 border-4 border-green-500">
                  <div className="text-center">
                    <div className="text-9xl mb-6">🏆</div>
                    <h1 className="text-5xl font-bold text-white mb-4">
                      ¡FELICIDADES!
                    </h1>
                    <div className="h-1 w-32 bg-green-500 mx-auto mb-6"></div>
                    <p className="text-2xl text-green-300 mb-6">
                      Has completado el Escape Room
                    </p>
                    <p className="text-xl text-white mb-8">
                      🎓 Ahora eres oficialmente un <strong className="text-yellow-400">Experto en Mecánica</strong>
                    </p>
                    <div className="bg-green-900/30 rounded-lg p-6 mb-6 border border-green-500/50">
                      <p className="text-green-200 text-lg">
                        Has demostrado tus habilidades en:
                      </p>
                      <ul className="text-white mt-4 space-y-2">
                        <li>✓ Colisiones y momento lineal</li>
                        <li>✓ Cinemática rotacional</li>
                        <li>✓ Energía y caída libre</li>
                      </ul>
                    </div>
                    <button
                      onClick={() => {
                        setCurrentRoom('inicio');
                        setInventory([]);
                        setAnswers({});
                        setBriefcaseCode(['', '', '', '']);
                      }}
                      className="bg-green-600 hover:bg-green-700 text-white font-bold py-4 px-8 rounded-lg transition-all transform hover:scale-105 flex items-center gap-3 mx-auto"
                    >
                      ↺ Jugar de Nuevo
                    </button>
                  </div>
                </div>
              </div>
            );
          }

          return null;
        };

        ReactDOM.render(<EscapeRoomFisica />, document.getElementById('root'));
    </script>
</body>
</html>
