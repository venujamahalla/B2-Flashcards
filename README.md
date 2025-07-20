# B2-Flashcards
import React, { useState, useEffect } from 'react';
import { ChevronLeft, ChevronRight, RotateCcw, Shuffle, BookOpen, Check, X } from 'lucide-react';

const flashcards = [
  { german: "die Aufregung", english: "excitement", example: "Die Aufregung vor der Prüfung war groß." },
  { german: "sich durchsetzen", english: "to assert oneself, to prevail", example: "Er konnte sich mit seiner Meinung durchsetzen." },
  { german: "der Anspruch", english: "claim, demand, standard", example: "Sie hat hohe Ansprüche an die Qualität." },
  { german: "bewältigen", english: "to cope with, to master", example: "Wir müssen diese Krise bewältigen." },
  { german: "die Gewohnheit", english: "habit", example: "Es ist eine schlechte Gewohnheit, zu spät zu kommen." },
  { german: "vertreten", english: "to represent, to substitute", example: "Er vertritt die Firma bei wichtigen Terminen." },
  { german: "die Auswirkung", english: "impact, effect", example: "Die Auswirkungen des Klimawandels sind spürbar." },
  { german: "einschätzen", english: "to assess, to estimate", example: "Ich kann die Situation noch nicht richtig einschätzen." },
  { german: "die Berechtigung", english: "authorization, justification", example: "Hat er die Berechtigung, hier zu parken?" },
  { german: "verzichten", english: "to do without, to renounce", example: "Ich verzichte auf Süßigkeiten." },
  { german: "die Verantwortung", english: "responsibility", example: "Als Chef trägt er große Verantwortung." },
  { german: "beeinträchtigen", english: "to impair, to affect negatively", example: "Der Lärm beeinträchtigt meine Konzentration." },
  { german: "die Nachfrage", english: "demand", example: "Die Nachfrage nach Bio-Produkten steigt." },
  { german: "erfassen", english: "to grasp, to record", example: "Alle Daten werden elektronisch erfasst." },
  { german: "die Beschwerde", english: "complaint", example: "Der Kunde reichte eine Beschwerde ein." },
  { german: "würdigen", english: "to appreciate, to honor", example: "Seine Leistung wurde angemessen gewürdigt." },
  { german: "die Genehmigung", english: "approval, permit", example: "Für den Umbau brauchen Sie eine Genehmigung." },
  { german: "berücksichtigen", english: "to take into account", example: "Wir müssen alle Faktoren berücksichtigen." },
  { german: "die Behauptung", english: "claim, assertion", example: "Diese Behauptung ist nicht bewiesen." },
  { german: "erweitern", english: "to expand, to extend", example: "Das Unternehmen möchte sein Angebot erweitern." },
  { german: "die Unterkunft", english: "accommodation", example: "Wir suchen eine günstige Unterkunft." },
  { german: "überzeugend", english: "convincing", example: "Seine Argumente waren sehr überzeugend." },
  { german: "die Verpflichtung", english: "obligation, commitment", example: "Wir haben eine Verpflichtung gegenüber unseren Kunden." },
  { german: "geringfügig", english: "minor, slight", example: "Es gab nur geringfügige Änderungen." },
  { german: "die Herausforderung", english: "challenge", example: "Das ist eine große Herausforderung für uns alle." },
  { german: "überwinden", english: "to overcome", example: "Wir müssen unsere Ängste überwinden." },
  { german: "die Entstehung", english: "origin, formation", example: "Die Entstehung des Universums ist ein Mysterium." },
  { german: "angemessen", english: "appropriate, adequate", example: "Die Bezahlung ist angemessen." },
  { german: "die Voraussetzung", english: "requirement, prerequisite", example: "Gute Deutschkenntnisse sind eine Voraussetzung." },
  { german: "betreuen", english: "to look after, to supervise", example: "Sie betreut die neuen Mitarbeiter." },
  { german: "die Untersuchung", english: "examination, investigation", example: "Die ärztliche Untersuchung ergab nichts Schlimmes." },
  { german: "beabsichtigen", english: "to intend", example: "Was beabsichtigen Sie mit dieser Maßnahme?" },
  { german: "die Vielfalt", english: "diversity, variety", example: "Die kulturelle Vielfalt bereichert unsere Gesellschaft." },
  { german: "verständlich", english: "understandable, comprehensible", example: "Seine Erklärung war sehr verständlich." },
  { german: "die Steigerung", english: "increase, improvement", example: "Die Steigerung der Produktivität ist unser Ziel." },
  { german: "befürworten", english: "to advocate, to support", example: "Ich befürworte diese Entscheidung vollkommen." },
  { german: "die Eigenschaft", english: "characteristic, property", example: "Flexibilität ist eine wichtige Eigenschaft." },
  { german: "vermeiden", english: "to avoid", example: "Wir sollten Konflikte vermeiden." },
  { german: "die Bevölkerung", english: "population", example: "Die Bevölkerung wächst stetig." },
  { german: "beitragen", english: "to contribute", example: "Jeder kann zum Erfolg beitragen." },
  { german: "der Umstand", english: "circumstance", example: "Unter diesen Umständen ist es schwierig." },
  { german: "ausüben", english: "to practice, to exert", example: "Er übt großen Einfluss auf das Team aus." },
  { german: "die Abweichung", english: "deviation, variance", example: "Es gibt eine Abweichung vom ursprünglichen Plan." },
  { german: "veranlassen", english: "to cause, to prompt", example: "Was hat Sie dazu veranlasst?" },
  { german: "die Einstellung", english: "attitude, employment", example: "Seine positive Einstellung gefällt mir." },
  { german: "erörtern", english: "to discuss, to debate", example: "Wir müssen das Problem ausführlich erörtern." },
  { german: "die Absicht", english: "intention", example: "Das war nicht meine Absicht." },
  { german: "vergleichbar", english: "comparable", example: "Die Ergebnisse sind nicht vergleichbar." },
  { german: "die Vereinbarung", english: "agreement, arrangement", example: "Wir haben eine Vereinbarung getroffen." },
  { german: "erläutern", english: "to explain, to clarify", example: "Können Sie mir das näher erläutern?" },
  { german: "die Betreuung", english: "care, supervision", example: "Die Betreuung der Kinder ist gewährleistet." },
  { german: "auffordern", english: "to call upon, to request", example: "Ich fordere Sie auf, zu schweigen." },
  { german: "der Zusammenhang", english: "connection, context", example: "Ich sehe keinen Zusammenhang zwischen den Ereignissen." },
  { german: "gering", english: "small, low", example: "Die Chancen sind gering." },
  { german: "die Stellungnahme", english: "statement, position", example: "Die Regierung gab eine Stellungnahme ab." },
  { german: "verfolgen", english: "to pursue, to follow", example: "Wir verfolgen eine klare Strategie." },
  { german: "die Ausstattung", english: "equipment, facilities", example: "Die technische Ausstattung ist modern." },
  { german: "auffällig", english: "conspicuous, striking", example: "Sein auffälliges Verhalten beunruhigte uns." },
  { german: "die Entwicklung", english: "development", example: "Die Entwicklung ist sehr erfreulich." },
  { german: "durchführen", english: "to carry out, to conduct", example: "Wir werden eine Umfrage durchführen." },
  { german: "der Vorgang", english: "process, procedure", example: "Dieser Vorgang dauert normalerweise eine Stunde." },
  { german: "bestätigen", english: "to confirm", example: "Können Sie den Termin bestätigen?" },
  { german: "die Begründung", english: "justification, reasoning", example: "Ihre Begründung ist nachvollziehbar." },
  { german: "entsprechen", english: "to correspond to, to meet", example: "Das entspricht nicht meinen Erwartungen." },
  { german: "die Regelung", english: "regulation, arrangement", example: "Es gibt eine neue Regelung für Homeoffice." },
  { german: "verschieden", english: "different, various", example: "Es gibt verschiedene Möglichkeiten." },
  { german: "die Grundlage", english: "basis, foundation", example: "Das ist die Grundlage unserer Zusammenarbeit." },
  { german: "erheblich", english: "considerable, significant", example: "Das ist ein erheblicher Unterschied." },
  { german: "die Behandlung", english: "treatment", example: "Die medizinische Behandlung war erfolgreich." },
  { german: "annehmen", english: "to assume, to accept", example: "Ich nehme an, dass Sie recht haben." },
  { german: "der Gegensatz", english: "contrast, opposite", example: "Das ist ein starker Gegensatz zu früher." },
  { german: "beteiligen", english: "to participate, to involve", example: "Möchten Sie sich an dem Projekt beteiligen?" },
  { german: "die Mitteilung", english: "message, communication", example: "Ich habe eine wichtige Mitteilung für Sie." },
  { german: "ursprünglich", english: "original, initially", example: "Ursprünglich wollten wir früher fahren." },
  { german: "die Vertretung", english: "representation, substitute", example: "Wer übernimmt Ihre Vertretung im Urlaub?" },
  { german: "übernehmen", english: "to take over, to assume", example: "Können Sie diese Aufgabe übernehmen?" },
  { german: "die Ausnahme", english: "exception", example: "Das ist eine seltene Ausnahme." },
  { german: "feststellen", english: "to determine, to notice", example: "Wir konnten einen Fehler feststellen." },
  { german: "die Vorstellung", english: "presentation, idea", example: "Ihre Vorstellung von Erfolg ist interessant." },
  { german: "verringern", english: "to reduce, to decrease", example: "Wir müssen die Kosten verringern." },
  { german: "die Erwartung", english: "expectation", example: "Die Erwartungen waren sehr hoch." },
  { german: "wesentlich", english: "essential, significant", example: "Das ist ein wesentlicher Punkt." },
  { german: "die Bedingung", english: "condition, requirement", example: "Unter welchen Bedingungen ist das möglich?" },
  { german: "beziehen", english: "to refer to, to obtain", example: "Worauf beziehen Sie sich?" },
  { german: "die Leistung", english: "performance, achievement", example: "Seine Leistung war außergewöhnlich." },
  { german: "verhindern", english: "to prevent", example: "Wir müssen den Unfall verhindern." },
  { german: "die Erfahrung", english: "experience", example: "Ich habe gute Erfahrungen mit diesem Produkt gemacht." },
  { german: "zusätzlich", english: "additional, extra", example: "Wir brauchen zusätzliche Informationen." },
  { german: "die Überlegung", english: "consideration, reflection", example: "Nach langer Überlegung entschied er sich." },
  { german: "bezeichnen", english: "to describe, to call", example: "Wie würden Sie das Problem bezeichnen?" },
  { german: "die Aussage", english: "statement, testimony", example: "Seine Aussage war sehr klar." },
  { german: "zurückführen", english: "to trace back to, to attribute", example: "Der Erfolg ist auf harte Arbeit zurückzuführen." },
  { german: "die Zustimmung", english: "approval, consent", example: "Wir brauchen Ihre Zustimmung für den Plan." },
  { german: "umfassen", english: "to include, to comprise", example: "Das Angebot umfasst alle Leistungen." },
  { german: "die Anforderung", english: "requirement, demand", example: "Die Anforderungen sind sehr hoch." },
  { german: "bewerten", english: "to evaluate, to assess", example: "Wie bewerten Sie die aktuelle Situation?" },
  { german: "die Darstellung", english: "presentation, portrayal", example: "Ihre Darstellung der Fakten ist korrekt." },
  { german: "ermöglichen", english: "to make possible, to enable", example: "Das neue System ermöglicht schnelleres Arbeiten." },
  { german: "die Überprüfung", english: "check, review", example: "Die Überprüfung der Dokumente ist notwendig." },
  { german: "voraussetzen", english: "to require, to assume", example: "Diese Position setzt Erfahrung voraus." }
];

const FlashcardApp = () => {
  const [currentCard, setCurrentCard] = useState(0);
  const [isFlipped, setIsFlipped] = useState(false);
  const [studyCards, setStudyCards] = useState(flashcards);
  const [showStats, setShowStats] = useState(false);
  const [correctCount, setCorrectCount] = useState(0);
  const [incorrectCount, setIncorrectCount] = useState(0);
  const [studiedCards, setStudiedCards] = useState(new Set());

  const shuffleCards = () => {
    const shuffled = [...studyCards].sort(() => Math.random() - 0.5);
    setStudyCards(shuffled);
    setCurrentCard(0);
    setIsFlipped(false);
  };

  const resetProgress = () => {
    setCurrentCard(0);
    setIsFlipped(false);
    setCorrectCount(0);
    setIncorrectCount(0);
    setStudiedCards(new Set());
    setStudyCards(flashcards);
  };

  const nextCard = () => {
    if (currentCard < studyCards.length - 1) {
      setCurrentCard(currentCard + 1);
      setIsFlipped(false);
    }
  };

  const prevCard = () => {
    if (currentCard > 0) {
      setCurrentCard(currentCard - 1);
      setIsFlipped(false);
    }
  };

  const markCard = (correct) => {
    if (correct) {
      setCorrectCount(correctCount + 1);
    } else {
      setIncorrectCount(incorrectCount + 1);
    }
    setStudiedCards(new Set([...studiedCards, currentCard]));
  };

  const flipCard = () => {
    setIsFlipped(!isFlipped);
  };

  const card = studyCards[currentCard];

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 p-4">
      <div className="max-w-4xl mx-auto">
        {/* Header */}
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold text-gray-800 mb-2 flex items-center justify-center gap-2">
            <BookOpen className="text-blue-600" />
            German B2 Flashcards
          </h1>
          <p className="text-gray-600">Master advanced German vocabulary with interactive practice</p>
        </div>

        {/* Stats Bar */}
        <div className="bg-white rounded-lg shadow-md p-4 mb-6">
          <div className="flex justify-between items-center text-sm">
            <span className="text-gray-600">
              Card {currentCard + 1} of {studyCards.length}
            </span>
            <div className="flex gap-4">
              <span className="text-green-600 flex items-center gap-1">
                <Check size={16} />
                Correct: {correctCount}
              </span>
              <span className="text-red-600 flex items-center gap-1">
                <X size={16} />
                Incorrect: {incorrectCount}
              </span>
            </div>
          </div>
          <div className="w-full bg-gray-200 rounded-full h-2 mt-2">
            <div 
              className="bg-blue-600 h-2 rounded-full transition-all duration-300"
              style={{ width: `${((currentCard + 1) / studyCards.length) * 100}%` }}
            ></div>
          </div>
        </div>

        {/* Main Flashcard */}
        <div className="mb-8">
          <div 
            className="bg-white rounded-xl shadow-lg p-8 min-h-80 cursor-pointer transition-all duration-300 hover:shadow-xl"
            onClick={flipCard}
          >
            <div className="text-center h-full flex flex-col justify-center">
              {!isFlipped ? (
                // German Side
                <div>
                  <div className="text-sm text-blue-600 mb-2 uppercase tracking-wide">German</div>
                  <h2 className="text-3xl font-bold text-gray-800 mb-4">{card.german}</h2>
                  <p className="text-gray-500">Click to reveal translation</p>
                </div>
              ) : (
                // English Side
                <div>
                  <div className="text-sm text-green-600 mb-2 uppercase tracking-wide">English</div>
                  <h2 className="text-3xl font-bold text-gray-800 mb-4">{card.english}</h2>
                  <div className="border-t pt-4 mt-4">
                    <div className="text-sm text-blue-600 mb-2 uppercase tracking-wide">Example</div>
                    <p className="text-lg text-gray-700 italic">{card.example}</p>
                  </div>
                </div>
              )}
            </div>
          </div>
        </div>

        {/* Controls */}
        <div className="flex justify-center gap-4 mb-6">
          <button
            onClick={prevCard}
            disabled={currentCard === 0}
            className="flex items-center gap-2 px-4 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
          >
            <ChevronLeft size={20} />
            Previous
          </button>
          
          <button
            onClick={flipCard}
            className="flex items-center gap-2 px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors"
          >
            <RotateCcw size={20} />
            Flip Card
          </button>
          
          <button
            onClick={nextCard}
            disabled={currentCard === studyCards.length - 1}
            className="flex items-center gap-2 px-4 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
          >
            Next
            <ChevronRight size={20} />
          </button>
        </div>

        {/* Knowledge Check Buttons */}
        {isFlipped && (
          <div className="flex justify-center gap-4 mb-6">
            <button
              onClick={() => markCard(false)}
              className="flex items-center gap-2 px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition-colors"
            >
              <X size={20} />
              Need Practice
            </button>
            <button
              onClick={() => markCard(true)}
              className="flex items-center gap-2 px-4 py-2 bg-green-500 text-white rounded-lg hover:bg-green-600 transition-colors"
            >
              <Check size={20} />
              Got It!
            </button>
          </div>
        )}

        {/* Action Buttons */}
        <div className="flex justify-center gap-4">
          <button
            onClick={shuffleCards}
            className="flex items-center gap-2 px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors"
          >
            <Shuffle size={20} />
            Shuffle Cards
          </button>
          
          <button
            onClick={resetProgress}
            className="flex items-center gap-2 px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition-colors"
          >
            <RotateCcw size={20} />
            Reset Progress
          </button>
        </div>

        {/* Study Tips */}
        <div className="mt-8 bg-white rounded-lg shadow-md p-6">
          <h3 className="text-xl font-semibold text-gray-800 mb-4">Study Tips</h3>
          <ul className="text-gray-600 space-y-2">
            <li>• Click on cards to flip between German and English</li>
            <li>• Use the "Got It!" and "Need Practice" buttons to track your progress</li>
            <li>• Shuffle cards regularly to test your knowledge in different orders</li>
            <li>• Focus on creating your own sentences with new words</li>
            <li>• Review difficult cards multiple times throughout your study session</li>
          </ul>
        </div>
      </div>
    </div>
  );
};

export default FlashcardApp;
