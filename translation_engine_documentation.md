# Oracle Bone Script Translation Engine Documentation
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Oracle Bone Script Translation Engine – Demo\n",
    "### with Mnemosyne Protocol Integration\n",
    "\n",
    "This notebook demonstrates the core functionality of the AlphaOracle translation engine and shows how the **Mnemosyne Protocol** (PHCA, BPA, Dante's Algorithm) can be applied to recover lost knowledge from ancient inscriptions.\n",
    "\n",
    "---"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 1. Installation\n",
    "\n",
    "If the package is published on PyPI, install it. Otherwise, ensure the local module is in your Python path."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "# !pip install alphaoracle  # uncomment if published"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 2. Import and Load the Translator"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "from alphaoracle import Translator\n",
    "\n",
    "# Initialize the translator (this may load a pre-trained model)\n",
    "translator = Translator()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 3. Translate a Sample Inscription\n",
    "\n",
    "Let's test with a simple modern Chinese representation of an oracle bone phrase (in practice, you would input the actual ancient glyphs)."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "text = \"王贞：下雨？\"  # \"The king divines: will it rain?\"\n",
    "result = translator.translate(text)\n",
    "print(\"Translation:\", result.text)\n",
    "print(\"Confidence:\", result.confidence)\n",
    "print(\"Alternatives:\", result.alternatives)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 4. Batch Translation\n",
    "\n",
    "Process multiple inscriptions at once."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "inscriptions = [\n",
    "    \"甲辰卜，贞：王出？\",\n",
    "    \"癸亥卜，争贞：今岁年？\",\n",
    "    \"贞：其雨？\"\n",
    "]\n",
    "results = translator.batch_translate(inscriptions)\n",
    "for i, res in enumerate(results):\n",
    "    print(f\"{i+1}. {res.text} (conf: {res.confidence})\")\n",
    "    if res.alternatives:\n",
    "        print(\"   alternatives:\", res.alternatives)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 5. Confidence Scoring and Alternative Readings\n",
    "\n",
    "Each translation includes a confidence score (0‑100) and a list of alternative interpretations. This is crucial for uncertain characters."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "for r in results:\n",
    "    print(f\"\\nTranslation: {r.text}\")\n",
    "    print(f\"Confidence: {r.confidence}\")\n",
    "    if r.alternatives:\n",
    "        print(\"Alternatives:\")\n",
    "        for alt in r.alternatives:\n",
    "            print(f\"  - {alt} (prob: {alt.probability})\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 6. Visualize an Oracle Bone (if images available)\n",
    "\n",
    "If you have an image of an oracle bone, you can overlay the detected characters and their translations."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "from alphaoracle import visualize\n",
    "\n",
    "# visualize.show_bone(\"path/to/bone.jpg\", overlay=result.characters)  # example"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "---\n",
    "\n",
    "# Applying the Mnemosyne Protocol\n",
    "\n",
    "The **Mnemosyne Protocol** uses three operations to recover corrupted knowledge. Here we demonstrate how they can be applied to an oracle bone inscription, turning a simple translation into a deeper understanding.\n",
    "\n",
    "We'll use a real (or simulated) fragmentary inscription:\n",
    "\n",
    "> \"...卜，贞：...方出，...受佑？\"\n",
    "\n",
    "(meaning \"... divined: ... the [Fang] tribes come out, ... receive divine assistance?\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Operation 1: Chronos – PHCA (Pattern‑Based Historical Context Analysis)\n",
    "\n",
    "**Layers:**\n",
    "- **Core:** What persists? The divination formula: date + \"卜\" + \"贞\" + question + often a prognostication. Invariant: the king consults ancestors about threats or resources.\n",
    "- **Infrastructure:** Physical evidence: the bone itself (turtle plastron), crack patterns, calligraphy style, excavation site (Xiaotun, Anyang).\n",
    "- **Niche:** Why here? Shang court divination was centralized at Yinxu; the topic (\"Fang\" tribes) indicates frontier conflict.\n",
    "- **Behavioral:** The diviner applied heat, interpreted cracks, inscribed the result. The king often participated.\n",
    "- **Cultural:** Stories of Shang kings and their enemies persisted in later texts (e.g., *Shiji*)."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "phca_output = {\n",
    "    \"core\": \"royal concern about enemy incursions\",\n",
    "    \"infrastructure\": \"turtle plastron, Shang script, crack pattern\",\n",
    "    \"niche\": \"Shang court divination, Yinxu site\",\n",
    "    \"behavioral\": \"diviner cracks bone, king interprets, scribe carves\",\n",
    "    \"cultural\": \"later historical records of Shang wars\"\n",
    "}\n",
    "print(\"PHCA Layers:\")\n",
    "for k, v in phca_output.items():\n",
    "    print(f\"  {k}: {v}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Operation 2: Logos – BPA (Bayesian Predictive Analysis)\n",
    "\n",
    "We hypothesize that the missing character before \"方出\" is a direction (e.g., \"土方\", \"鬼方\") or a verb. Using the engine's confidence scores and prior probabilities from known inscriptions, we can update our belief."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "from alphaoracle import BayesianUpdater\n",
    "\n",
    "# Suppose the engine returns three possibilities for the missing character:\n",
    "candidates = [\n",
    "    {\"char\": \"土\", \"prob\": 0.6, \"meaning\": \"Tu (a tribe)\"},\n",
    "    {\"char\": \"鬼\", \"prob\": 0.3, \"meaning\": \"Gui (demon tribe)\"},\n",
    "    {\"char\": \"𢀛\", \"prob\": 0.1, \"meaning\": \"unknown\"}\n",
    "]\n",
    "\n",
    "# Prior based on frequency in corpus (e.g., 土 appears 40%, 鬼 20%, other 40%)\n",
    "prior = {\"土\": 0.4, \"鬼\": 0.2, \"other\": 0.4}\n",
    "\n",
    "# Update using Bayes (simplified – normally would use Dirichlet-multinomial)\n",
    "posterior = {}\n",
    "for c in candidates:\n",
    "    char = c[\"char\"]\n",
    "    like = c[\"prob\"]\n",
    "    post = (prior.get(char, 0.4) * like) / sum(prior.get(ch, 0.4) * like for ch in [c[\"char\"] for c in candidates])\n",
    "    posterior[char] = post\n",
    "\n",
    "print(\"Posterior probabilities for missing character:\")\n",
    "for char, prob in posterior.items():\n",
    "    print(f\"  {char}: {prob:.3f}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Operation 3: Katharsis – Dante's Algorithm\n",
    "\n",
    "Now we strip away later misinterpretations and let the fragments reorient.\n",
    "\n",
    "**Inferno:** Burn the official story – e.g., early 20th-century scholars misread \"方\" as \"country\" rather than a specific tribal confederation.\n",
    "\n",
    "**Purgatorio:** Let the fragments speak – compare this inscription with dozens of others mentioning \"方\". Notice that they often co-occur with military verbs and place names.\n",
    "\n",
    "**Paradiso:** Recognize the invariant – the inscription is part of a systematic record of Shang‑Fang relations, revealing a long‑term conflict pattern.\n",
    "\n",
    "Below we simulate a simple textual output of this process."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "def dante_algorithm(inscription):\n",
    "    print(\"=== Inferno ===\")\n",
    "    print(\"Burning away: post‑Shang reinterpretations, Confucian moralizing, modern nationalist biases.\")\n",
    "    print(\"\\n=== Purgatorio ===\")\n",
    "    print(\"Gathering fragments: 27 other inscriptions mentioning 'Fang'. They cluster around the reigns of Wu Ding and Zu Geng.\")\n",
    "    print(\"\\n=== Paradiso ===\")\n",
    "    print(\"Invariant recognized: The Fang were a persistent enemy; the king repeatedly sought ancestral guidance.\")\n",
    "    print(\"Testimony: The oracle bones are not superstition – they are intelligence reports.\")\n",
    "\n",
    "dante_algorithm(\"...卜，贞：...方出，...受佑？\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 7. Putting It All Together\n",
    "\n",
    "The Mnemosyne Protocol doesn't replace the translation engine; it guides **how** to interpret its output. By combining PHCA (the historical layers), BPA (probabilistic reasoning), and Dante's Algorithm (transformative reading), we recover not just the words, but their meaning and significance.\n",
    "\n",
    "The final step is **Testimony** – publishing the restored knowledge so it enters living tradition."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "print(\"\\nTESTIMONY:\\nThe oracle bones are not dead. They are witnesses. We have read them.\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "---\n",
    "## End of Demo\n",
    "\n",
    "This notebook demonstrated both the technical translation engine and the philosophical recovery framework. Together they form a powerful tool for unlocking the past.\n",
    "\n",
    "*Recover what was lost. Witness what was silenced.*"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.0"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
## Implementation
The Oracle Bone Script Translation Engine is designed to process ancient Chinese characters from oracle bone inscriptions. The engine employs several NLP techniques and libraries to achieve accurate translations.

## Analysis
The translations generated by the engine have been evaluated using a small set of modern Chinese translations for comparison. The results show a high degree of correlation, but there are still areas for improvement.

## Limitations
1. **Accuracy**: The engine's accuracy decreases for rare characters due to limited training data.
2. **Context Sensitivity**: The engine struggles with idiomatic expressions and context-specific meanings.
3. **Performance**: Current implementation can be slow with large text inputs.

## Recommendations for Improvement
1. **Enhance Training Dataset**: Increase the diversity and quantity of training examples.
2. **Contextual Analysis**: Incorporate techniques that consider the context of words.
3. **Optimize Performance**: Refactor the code to improve processing speed and efficiency.

## Code Structure
- **Main Script**: Contains the core translation logic and algorithms.
- **Data Handling**: Scripts for loading, cleaning, and preprocessing training data.
- **Evaluation**: Scripts for testing accuracy against a test dataset.

## Functionality
The engine translates oracle bone characters to modern Chinese characters, providing insights into character meaning and usage within historical contexts.

## Strengths
- Effective for common characters.
- Provides detailed commentary on translations.

## Suggested Enhancements
- Implement parallel processing for large datasets.
- Develop a web interface for broader accessibility and user engagement.

This documentation serves as a foundation for future enhancements to the Oracle Bone Script Translation Engine. 
