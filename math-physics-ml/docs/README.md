# Example Prompts by Discipline

Hundreds of natural language prompts organized by field. Just describe what you want—no need to know the underlying APIs.

## Available Example Collections

| Document | Topics | Example Count |
|----------|--------|---------------|
| [Physics](examples-physics.md) | Mechanics, E&M, Quantum, Relativity, Fluids, Optics, Nuclear, Condensed Matter, Plasma, Astrophysics | ~130 |
| [Chemistry](examples-chemistry.md) | Quantum Chem, MD, Kinetics, Spectroscopy, Electrochemistry, Polymers, Biochemistry | ~100 |
| [Mathematics](examples-mathematics.md) | Calculus, Linear Algebra, ODEs/PDEs, Number Theory, Probability, Numerical Methods, Algebra, Topology | ~130 |
| [Machine Learning](examples-ml-ai.md) | Language Models, Transformers, Vision, Genertic Models, RL, GNNs, Self-Supervised, Interpretability | ~130 |
| [Engineering](examples-engineering.md) | Structural, Mechanical, Electrical, Control, Signal Processing, Aerospace, Chemical, Biomedical, Robotics | ~120 |
| [Biology](examples-biology.md) | Systems Bio, Population Dynamics, Evolution, Molecular, Bioinformatics, Neuroscience, Ecology, Epidemiology | ~120 |
| [Finance](examples-finance.md) | Options, Portfolio, Fixed Income, Risk, Derivatives, Algo Trading, Macro/Micro Economics, Econometrics | ~130 |
| [Data Science](examples-data-science.md) | EDA, Statistics, Regression, Clustering, NLP, Recommenders, A/B Testing, Causal Inference, Survival | ~130 |

**Total: ~1000+ example prompts**

## How to Use

1. Find your domain in the table above
2. Browse the examples for prompts similar to your task
3. Copy and modify for your specific needs
4. The AI will handle the implementation details

## Example Workflow

**You want to:** Analyze the stability of a protein-ligand complex

**You find in Biology → Structural Biology:**
> "Analyze protein dynamics with normal modes"
> "Model ligand binding affinity"

**You ask:**
> "Compute the normal modes of my protein structure and analyze how the binding site fluctuates. Then estimate the binding free energy for the docked ligand."

The system handles:
- Loading structure files
- Setting up the calculation
- Running normal mode analysis
- Computing binding energies
- Visualizing results

## Contributing Examples

Have domain expertise? Add examples to help others:

1. Fork the repository
2. Add prompts to the relevant `examples-*.md` file
3. Keep prompts concise and conceptually clear
4. Submit a pull request
