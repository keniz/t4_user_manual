# ECOF

ECOF is intended for non-isothermal flow and transport of water, CO₂, CH₄, H₂S, and multicomponent oil mixtures, with applications to oil and gas production, enhanced oil recovery (EOR), and geological carbon sequestration in depleted oil and gas reservoirs. The module is formulated as a fully compositional model. Phase behavior and thermophysical properties of the gas and oil phases are calculated using the Peng–Robinson equation of state (PR-EOS, Peng and Robinson, 1976), while a mixing-based approach is employed to estimate aqueous-phase thermophysical properties. Phase equilibrium, including the appearance and disappearance of gas, oil, and aqueous phases, as well as the partitioning of non-aqueous components (e.g., CO₂, CH₄, and oil components) among coexisting phases, is modeled using the equal-fugacity principle through an efficient flash-calculation algorithm. Saturated water vapor pressure and water solubility in the oil phase are incorporated to model partitioning of the H₂O component between gas and oil phases. All components are allowed to exist in all three phases (aqueous, gaseous, and oil).

**1  Components**

ECOF is originally intended for flow and transport of water, CO₂, CH₄, H₂S, and black oil mixtures. The module is formulated as a fully compositional model and theoretically speaking it allows including any hydrocarbon components. H2O is the default component in any simulation. Any combination of non-condensable gases and hydrocarbon components is allowed. In addition, as many as 5 tracers may also be included, which are supposed to be small fractions and do not have an impact on thermophysical properties of the fluid. In this report, the collective name “hydrocarbon components” refers to all the formal hydrocarbon components and non-condensable gases (such as CO<sub>2</sub> and  H<sub>2</sub>S). The total number of components for an ECOF simulation is the sum of number of hydrocarbon components, number of tracers and water.&#x20;

TOUGH4 maintains an internal database for 22 hydrocarbon components. The database provides key parameters for those components. However, not all parameters needed for modeling are available and reliable for all components in the database. The parameters include following groups:

“A”: Basic parameters (e.g. molar weight, critical parameters, Pitzer's acentric factor and others),

“B”: Binary interaction coefficients,

“C”: Parameters for calculation of solubility in water,

“D”  Peneloux  correction volume.

Table 2-1 provides a list of the components available in the internal database and parameters for each component.

_Table 2-1 The components that are defined internally and parameters provided_

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Components</td><td valign="top">Symbols<sup>1</sup></td><td valign="top">Parameters<sup>2</sup></td></tr><tr><td valign="top">METHANE</td><td valign="top">CH4</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">ETHANE</td><td valign="top">C2H6</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">PROPANE</td><td valign="top">C3H8</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">HYDROGEN SULFIDE</td><td valign="top">H2S</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">CARBON DIOXIDE</td><td valign="top">CO2</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">NITROGEN</td><td valign="top">N2</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">OXYGEN</td><td valign="top">O2</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">WATER</td><td valign="top">H2O</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">METHANOL</td><td valign="top">CH4O</td><td valign="top">A, B,   , D</td></tr><tr><td valign="top">n-BUTANE</td><td valign="top">C4H10</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">n-PENTANE</td><td valign="top">C5H12</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">n-HEXANE</td><td valign="top">C6H14</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">i-BUTANE</td><td valign="top">iC4H10</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">i-PENTANE</td><td valign="top">iC5H12</td><td valign="top">A, B, C, D</td></tr><tr><td valign="top">n-HEPTANE</td><td valign="top">C7H16</td><td valign="top">A, B, C-, D</td></tr><tr><td valign="top">n-OCTANE</td><td valign="top">C8H18</td><td valign="top">A, B, C-, D</td></tr><tr><td valign="top">n-NONANE</td><td valign="top">C9H20</td><td valign="top">A, B,     , D</td></tr><tr><td valign="top">n-DECANE</td><td valign="top">C10H22</td><td valign="top">A, B,    , D</td></tr><tr><td valign="top">BENZENE</td><td valign="top">C6H6</td><td valign="top">A,         , D</td></tr><tr><td valign="top">SULPHUR DIOXIDE</td><td valign="top">SO2</td><td valign="top">A,         , D</td></tr><tr><td valign="top">NITROGEN OXIDE</td><td valign="top">NO2</td><td valign="top">A,         , D</td></tr><tr><td valign="top">HYDROGEN</td><td valign="top">H2</td><td valign="top">A, B-, C, D</td></tr></tbody></table>

1\.       used to identify the component in the input file (see input keyword “CHEMP”).

2\.       “–“ sign indicates that the data quality may be not reliable.

The user can also use hydrocarbon components other than those in the default database by defining them in the input file as pseudo-components and providing their parameters through input keyword “CHEMP”. The default parameters provided in the database for any component can be replaced through input file.

**2  Thermophysical properties of oil and gas phases**

This section describes the algorithms used in ECOF to evaluate thermophysical properties of the non‑aqueous phases (gas and oil) for multicomponent mixtures. ECOF computes phase densities, viscosities, and specific enthalpies as functions of pressure P, temperature T, and phase composition. The methodology follows a Peng–Robinson (PR) equation‑of‑state framework with robust selection of compressibility‑factor roots and optional liquid density corrections via volume translation.

**2.1 Scope and general workflow**

ECOF evaluates thermophysical properties of the non-aqueous phases (gas and oil) as functions of pressure , temperature , and phase composition (or ). The primary properties required by the flow and transport equations are:

* Density  of gas and oil phases,
* Viscosity of gas and oil phases,
* Specific enthalpy of gas and oil phases.

The overall workflow implemented is:

1. Compute pure-component PR parameters from critical properties and acentric factor.
2. Apply temperature dependence via , and form mixture parameters using mixing rules and binary interaction coefficients .
3. Solve the Peng–Robinson cubic EOS in terms of compressibility factor .
4. If multiple real roots exist, apply root selection consistent with the target phase (gas/oil) and, if needed, a stability criterion based on Gibbs free energy.
5. Compute density from , then (optionally) apply a liquid density correction using volume translation.
6. Compute viscosity using either a corresponding-states method (fallback/low ) or a friction-theory method consistent with the EOS.
7. Compute enthalpy using ideal-gas enthalpy + EOS departure (residual) enthalpy.
8. &#x20;

2.4.2 Peng–Robinson EOS and mixing rules

For the non-aqueous phases, ECOF uses the Peng–Robinson (PR) EOS to represent real-fluid behavior of hydrocarbon/gas mixtures:

&#x20;                                                                           (2-10)

where:

* &#x20;is pressure,
* &#x20;is temperature,
* &#x20;is the universal gas constant,
* &#x20;is molar volume,
* and  are EOS parameters.

Pure‑component parameters for component _i_ are:

&#x20;,        &#x20;

Temperature dependence is introduced by:

&#x20;            &#x20;

Mixture parameters for phase composition are computed using van der Waals mixing rules:

,

,         &#x20;

2.4.3 Cubic EOS solution and root selection

Define reduced EOS parameters:

The PR EOS can be expressed as a cubic equation in compressibility factor Z = PV/(RT):

&#x20;                            (2-11)&#x20;

Physical admissibility requires Z > B (equivalently V > ) to avoid singularities in ln(Z − B) terms and to keep V –  > 0. When multiple admissible roots exist, ECOF uses:

• Gas phase (β = g): the largest admissible root (gas‑like root).

• Oil phase (β = o): the smallest admissible root (liquid‑like root).

If phase identity is not fixed a priori, a stability criterion can be applied based on the difference of dimensionless Gibbs free energy between the smallest root _Z_<sub>_b_</sub> and largest root _Z_<sub>_a_</sub> (Nghiem and Li, 1989):

&#x20;                         (2-12)

where δ1 = 1 +  and δ2 = 1 – . Select _Z_<sub>b</sub> if ΔG > 0; otherwise select _Z_<sub>a</sub>.

2.4.4 Densities and liquid density correction

For a selected , the mass density is:

&#x20;                                                                                                                      (2-13)

_MW_ is molar weight of the mixture.  To improve liquid (oil‑phase) density predictions without changing phase equilibria, ECOF supports a volume‑translation (volume‑shift, Peneloux et al. 1982) correction. The corrected molar volume is:

&#x20;                                                           (2-14)

and the corrected oil density is:

&#x20;                                                                                                                     (2-15)                                      &#x20;

Here _c_<sub>_i_</sub> is a component‑specific volume shift parameter (optionally temperature‑dependent). The correction is applied only to density (and derived quantities) so that fugacity coefficients and flash calculations remain consistent with the underlying PR EOS.

An alternative approach has also been implemented in ECOF based on  Lin and Duan (2005). It applies to a temperature-dependent translation. This approach is used to better match liquid densities over broader conditions, while keeping the EOS phase behavior unchanged.

2.4.5 Viscosity

TOUGH4 implements two complementary viscosity models for non-aqueous phases (gas and oil):\
(1) a corresponding-states viscosity model after Chung et al. (1988), and\
(2) a friction-theory viscosity model after Quiñones-Cisneros et al. (2000, 2001).

The two models are used in a hierarchical and complementary manner to ensure both numerical robustness and accuracy over a wide range of pressures, temperatures, and phase states.

The Chung et al. (1988) method is used in ECOF to compute dilute-gas and moderate-density viscosities, and it also serves as a fallback model when friction-theory parameters are unavailable or when numerical robustness is prioritized.

In this approach, the viscosity of each pure component is evaluated using a corresponding-states formulation based on critical properties and the acentric factor. The dilute-gas viscosity of component is expressed as:

&#x20;                                                                                                      (2-16)

where is the reduced temperature, is the acentric factor, and is the molecular weight. Dense-gas corrections are incorporated through empirically fitted shape factors as described by Chung et al. (1988).

For multicomponent mixtures, the dilute-gas mixture viscosity is computed using a Wilke-type mixing rule:

&#x20;                                                                                                       (2-17)\
<br>

where is the mole fraction of component in phase , and is the Wilke interaction parameter depending on component viscosities and molecular weights.

The Chung model is applied in ECOF for:

* Gas-phase viscosity at low to moderate densities,
* Initial estimates for viscosity in nonlinear iterations,
* Fallback calculations when friction-theory coefficients are unavailable.

For high-pressure, dense-fluid, and liquid-like conditions, ECOF employs the friction-theory viscosity model developed by Quiñones-Cisneros et al. (2000, 2001). This method is fully consistent with cubic equations of state and is the default viscosity model for the oil phase in ECOF.

In friction theory, the total viscosity is decomposed as:

&#x20;                                                                                                                  (2-18)      \
where:

* is the dilute-gas mixture viscosity computed using the Chung et al. (1988) method,
* is an additional friction contribution accounting for dense-fluid effects.

The friction term is expressed as a function of attractive and repulsive pressure contributions derived consistently from the Peng–Robinson EOS:

&#x20;                                                                (2-19)        \
The friction contribution is modeled as:

where , , and are mixture-dependent coefficients obtained from component parameters and composition-weighted mixing rules.

This formulation allows viscosity to increase smoothly with pressure and density and ensures thermodynamic consistency between viscosity and the underlying EOS used for phase behavior and density calculations.

The friction-theory model is applied in ECOF for:

* Oil-phase viscosity,
* Dense gas and near-critical conditions,
* High-pressure reservoir simulations relevant to EOR and CO₂ storage.

2.4.6 Specific enthalpy

Specific enthalpy of the non‑aqueous phase is computed as:

&#x20;                                                         (2-20)&#x20;

The ideal‑mixture enthalpy is obtained from temperature‑dependent ideal‑gas heat capacities for each component, integrated from a reference state ( ).

The departure enthalpy  accounts for real‑fluid effects and is evaluated from a PR departure function that depends on, A, B, and the temperature derivative . A commonly used PR form is:

&#x20;                                              (2-21)

2.4.7 Numerical robustness considerations

Cubic EOS property evaluation must be numerically robust because it is called repeatedly inside Newton iterations and strongly affects Jacobian quality. ECOF includes the following safeguards:

• Root filtering and admissibility: discard roots with Z ≤ B (or V ≤ ). For near‑singular states, enforce a small positive margin Z − B ≥ ε to avoid ln(Z − B) blow‑up in fugacity and departure functions.

• Stable root selection: when multiple admissible roots exist, select Z based on phase identity (largest for gas, smallest for oil) and, when phase identity is uncertain, use a Gibbs‑energy criterion to avoid metastable roots.

• Single‑root (supercritical) handling: if only one admissible root exists, treat the state as single‑phase and use that root consistently to prevent artificial phase switching.

• Continuity across phase changes: during flash iterations and during appearance/disappearance of phases, apply consistent root selection and optional damping/“phase stickiness” (if enabled elsewhere in ECOF) so that Z, ρ, μ, and h vary smoothly, improving Newton convergence.

• Bounded volume translation: apply volume‑shift correction only to liquid density and enforce V\_corr > 0. If the computed shift would make V\_corr unrealistically small/negative under extreme conditions, cap the shift or fall back to EOS density to maintain physical consistency.

• Log/ratio protections: when evaluating ln\[(Z + δ<sub>1</sub> B)/(Z + δ<sub>2</sub> B)] or similar expressions, enforce lower bounds on arguments to avoid invalid floating‑point operations.

• Graceful fallback: if viscosity/enthalpy submodels require parameters not available for a user‑defined component, use a simplified correlation (e.g., Arrhenius‑type viscosity or ideal‑mixture enthalpy) with smooth blending, rather than failing the Newton step.

These measures are particularly important for ECOF applications near critical conditions, in highly compressible gas–oil mixtures, and in simulations with strong coupling among flow, phase behavior, and energy transport.

2.3  Flash calculation.

The flash-calculation algorithm implemented in the ECOF module to determine gas–oil phase split and phase compositions at given pressure and temperature. The implementation is contained in the Fortran module flash\_module (FlashCalculation.f90) and is designed for repeated use inside TOUGH4’s fully implicit Newton iterations. The routine accepts an overall composition vector and an initial estimate of equilibrium ratios (K-values) and returns the vapor (gas) fraction, the liquid (oil) and vapor (gas) compositions, and a phase flag indicating single-phase or two-phase state.

In ECOF, thermodynamic equilibrium between the gas and oil phases is modeled using equality of component fugacities. Fugacity coefficients are evaluated with the same Peng–Robinson EOS routines used for density, viscosity, and enthalpy. For numerical robustness, the flash routine uses (i) endpoint phase tests, (ii) a safeguarded Newton/bisection solver for the Rachford–Rice equation, and (iii) additional stabilization controls that suppress spurious “micro-phases” and reduce phase-chattering near boundaries.

2.5.1 Notation and flash problem definition

The flash calculation treated here is a two-phase (gas–oil) equilibrium problem at specified pressure P and temperature T. Let i = 1,…,Nc index the components participating in the PR-EOS gas–oil equilibrium subsystem. The flash routine uses the standard compositional notation:

• z<sub>i</sub> : overall (feed) mole fraction of component _i_ in the gas–oil subsystem ( );

• x<sub>i</sub> : oil-phase (liquid) mole fraction ( );

• y<sub>i</sub> : gas-phase (vapor) mole fraction ( );

• β : gas-phase molar fraction, 0 ≤ β ≤ 1.

For a given (P, T, z<sub>i</sub>), the flash problem consists of finding β, x<sub>i</sub>, and y<sub>i</sub> such that (i) component mass conservation is satisfied and (ii) gas–oil phase equilibrium holds for all components. In the ECOF implementation, water partitioning between gas and oil is handled by dedicated correlations outside this PR flash; for compatibility with the EOS data structure, the fugacity routine allocates an extra composition slot but sets it to zero when computing PR fugacities for the Nc components.

2.5.2 Fugacity-based equilibrium ratios (K-values)

Gas–oil equilibrium is enforced through equality of component fugacities. For component _i_, the fugacity in phase α ∈ {L, V} can be written as , where  is the fugacity coefficient obtained from the EOS. Equilibrium between gas (V) and oil (L) implies , which leads to the definition of an equilibrium ratio . Using fugacity coefficients, ECOF updates K-values as:

&#x20;                                                                                                                      （2-22）

Equation (2--22) is the convention used in FlashCalculation.f90: after computing fugacity coefficients for the oil and gas roots of the PR EOS, the routine sets  with safeguards that bound K<sub>i</sub> to a wide but finite interval ( ) to prevent numerical overflow.

2.5.3 Rachford–Rice formulation for phase split

Given a set of K-values, the phase split is obtained from overall mass balance. Using  and  the phase compositions can be expressed as functions of β:

&#x20;                                                                                       （2-23）

Imposing yields the Rachford–Rice equation for β:

&#x20;                                                                                                                                                 (2-24）                                                                                                           &#x20;

The derivative used for Newton updates is:

&#x20;                                                                                                                                                 (2-25)

In ECOF, F(β) is solved with a safeguarded Newton–Raphson method constrained to 0 ≤ β ≤ 1. When Newton proposes a β outside the current bracket, the algorithm falls back to bisection. This ensures a physically admissible β and stable convergence inside Newton iterations of the flow solver.

2.5.4 Implementation of flash calculation

The routine for flash calculation in TOUGH4 (in FlashCalculation.f90) implements an outer loop that iterates on K-values, and for each K-update solves the Rachford–Rice equation for β. The routine also evaluates endpoint functions to detect single-phase states and to decide whether the two-phase solver should be activated. Two endpoint tests are evaluated from the current K-vector:

&#x20;                                                                              (2-26)

In terms of the Rachford–Rice function, f0 corresponds to F(β) evaluated at β = 0, while f1 corresponds to −F(β) evaluated at β = 1. These values provide a robust single-phase / two-phase classification: if both f0 and f1 are negative the mixture is liquid-only, if both are positive it is vapor-only, and mixed signs indicate that a two-phase root may exist within (0,1).

A practical challenge in fully implicit compositional simulation is that the K-vector available at intermediate Newton states (or at the start of a time step) may be inaccurate. If single-phase decisions are made immediately using a poor K guess, the routine can misclassify a cell as liquid-only or vapor-only, causing discontinuities when the phase state later corrects itself. To mitigate this, the ECOF flash routine performs a short sequence of “endpoint preconditioning” updates before finalizing single-phase decisions.

Specifically, when the endpoint tests suggest a single-phase region, the code carries out up to a small fixed number of iterations ( = 8) in which K-values are updated using fugacity ratios at an endpoint composition. For a likely liquid-only state, it sets β = 0 and uses x = z together with y proportional to Kx, then computes fugacity coefficients for both endpoints and updates . For a likely vapor-only state, it sets β = 1 and uses y = z together with x proportional to z/K, then performs the same fugacity-based K update. These inexpensive endpoint updates substantially improve bubble/dew discrimination without invoking the full two-phase solver.

In addition, the routine uses the phase state from the previous call as hysteresis information. When the endpoint tests are near zero (i.e., very close to the boundary within roundoff), the code avoids switching a previously-liquid cell to vapor or vice versa. The following thresholds are applied in the current implementation: f0\_on = 1×10⁻⁷ and f1\_on = 1×10⁻⁶ for turning on a new phase from a previous single-phase state, and f0\_vap\_on = 1×10⁻⁷ and f1\_vap\_on = 1×10⁻⁷ for switching to an all-vapor classification. When the state is ambiguous, the routine retains the previous phase when possible; otherwise it biases toward liquid to avoid creating spurious gas.

When the endpoint tests indicate a genuine possibility of two-phase behavior and the hysteresis conditions allow two-phase activation, the routine enters the two-phase path and solves Eq. (2-24) for β. The implementation uses a bracketed Newton scheme with initial bracket \[0,1]. At each inner iteration, the algorithm evaluates F(β) and F'(β) using Eqs. (2-24) and (2-25), computes a Newton trial β<sub>try</sub> = β − F/F', and enforces β<sub>try</sub> ∈ (β<sub>L</sub>, β<sub>R</sub>) by replacing out-of-bracket proposals with the bisection midpoint. The bracket is then updated using the sign of F evaluated at the accepted β<sub>try</sub>. This bracket update is performed using the freshly computed F(β<sub>try</sub>), ensuring that the bracket moves consistently and avoids incorrect endpoint updates.

The inner β solver uses a tight tolerance (tol\_beta = 1×10⁻¹⁰) and a maximum of max\_itB = 100 iterations. After β is determined, oil and gas compositions are computed from Eq. (2-23) and normalized to enforce . These compositions are then passed to the fugacity routines for K updating.

Fugacity coefficients are computed by the helper routine compute\_fugacity. This routine calls the PR-EOS driver (Z\_RealGas1) to obtain both liquid-root and gas-root compressibility factors (Z<sub>liq</sub> and Z<sub>gas</sub>) for the specified composition. Depending on the phase condition, the routine selects the corresponding Z and performs a physical admissibility check Z > B + ε (with ε ≈ 10⁻¹²) to avoid logarithm singularities. Fugacity coefficients φ<sub>i</sub> are then obtained by calling Fugacity(…) subroutine from the HydroCarbon\_properties module.

With and available, K-values are updated using Eq. (2-22). The implementation applies wide bounds (Kmin = 10⁻¹², Kmax = 10¹²) and preserves the previous K value if an EOS failure is detected for a component. No additional relaxation is applied in the main flash routine; instead, the outer loop convergence check controls iteration count and the surrounding TOUGH4 Newton solver provides global damping when needed.

The flash routine iterates on K-values in an outer loop with a maximum of max\_iter\_outer = 50 iterations. After each K update, convergence is evaluated using the maximum relative change across components:

&#x20;                                                                                                                                       (2-27)

If err\_max falls below tol\_outer = 1×10⁻⁶, the K-iteration stops and the routine returns β, x, y, and an updated phase\_flag. If the outer loop reaches its iteration limit without meeting the tolerance, the routine sets ierr = 1 to signal nonconvergence, but still returns the latest estimates so that the calling code can proceed with TOUGH4’s global nonlinear controls.

2.5.5 Numerical stabilization measures and summary

Two additional stabilization measures are applied after the outer loop. First, ECOF suppresses spurious “micro-phases” by snapping extremely small or extremely large vapor fractions to single-phase states. Specifically, if β < beta\_cut (beta\_cut = 1×10⁻¹⁰) the routine sets β = 0, and if 1−β < beta\_cut it sets β = 1. This reduces saturation noise and phase-chattering in cells that hover near phase boundaries, which is important for stable Jacobian evaluation.

Second, the routine uses the previous phase\_flag (passed in by reference) to impose a mild hysteresis: two-phase behavior is not activated unless the endpoint tests cross the bubble/dew conditions by more than small thresholds. This is particularly important because flash calculations are performed at intermediate Newton states that do not yet satisfy the fully converged solution, and abrupt phase switching at those intermediate states can degrade convergence.

In summary, the ECOF flash algorithm combines a fugacity-based thermodynamic formulation with practical numerical safeguards tailored for fully implicit multiphase flow simulation. The implementation uses EOS-consistent fugacity coefficients to update K-values, a safeguarded Newton/bisection solver for the Rachford–Rice equation, endpoint preconditioning to reduce misclassification when initial K guesses are imperfect, and phase-hysteresis/micro-phase cutoffs to suppress phase-chattering near boundaries. Together, these measures provide a robust phase-split calculation suitable for repeated calls inside TOUGH4 Newton iterations.

&#x20;

&#x20;

2.4  Thermophysical properties of the aqueous phase.

In ECOF, the aqueous phase is treated as liquid water that may contain dissolved non‑aqueous components (e.g., CO₂) and dissolved tracers/solutes (e.g., brine treated as a tracer). The pure water properties (density and internal energy, viscosity) are obtained from the standard TOUGH4 water property routines and are not repeated here. The focus of this section is the additional treatment implemented in ECOF to represent the impact of dissolved components on aqueous‑phase density and enthalpy, and the manner in which aqueous viscosity is used in the current implementation.

The dominant impact of dissolved components on the aqueous phase is represented through a correction to the aqueous density using an additive‑volume (specific‑volume mixing) approximation. The implementation follows the principle that the mixture molar specific volume is the mole‑fraction‑weighted sum of component molar specific volumes. The correction is applied in two steps: (i) a correction for dissolved tracer/solute components with prescribed densities, and (ii) an additional correction for dissolved CO₂ using a dedicated correlation.

(i)  Tracer/solute contribution. Let x<sub>k,a</sub> denote the aqueous mole fraction of tracer/solute component k (k = 1,…,Ntracer). For each tracer with a valid density provided in the tracer data input, ECOF computes an effective tracer molar density ρ<sub>k,m</sub> by converting the stored mass density to a molar density using the tracer molecular weight. Defining xtr = Σ x<sub>k,a</sub> (summed only over tracers with valid densities), the aqueous molar density after tracer correction is computed as:

&#x20;                                                                                               (2-28)

Tracers without a specified density are not included in the calculation using eq. (2-28) and therefore do not change the aqueous density (i.e., they are treated as dilute tracers with negligible volume effect).

(ii) CO₂ contribution. Because CO₂ dissolution can produce measurable aqueous density changes and because the apparent molar volume of dissolved CO₂ differs from that of bulk CO₂, ECOF applies a separate correction when CO₂ is present in the aqueous composition:

&#x20;                                                                                                           (2-29)

where _x_<sub>_CO2_</sub> is the mole fraction of CO<sub>2</sub> component in the aqueous phase, _ρ_<sub>_aq0_</sub> is the density of pure water with correction of the dissolved tracers, and _ρ_<sub>_CO2_</sub> is the density of CO<sub>2</sub> which is calculated as a function of temperature from the correlation for molar volume of dissolved CO<sub>2</sub> at infinite dilution developed by García (2001).

In the current ECOF implementation, CO₂ is the only dissolved gas treated with this dedicated density correction; the impact of other dissolved gases/hydrocarbons on aqueous density is neglected, which is typically acceptable because their aqueous concentrations are small under many reservoir conditions.

In the present ECOF implementation, the aqueous‑phase viscosity used in flow calculations is set equal to be pure liquid‑water viscosity, i.e., no additional viscosity correction is applied for dissolved gases or tracer/solute components within ECOF itself. This choice reflects a pragmatic balance between robustness and complexity and is consistent with many compositional reservoir workflows where aqueous viscosity changes due to dissolved gases are small compared to the dominant viscosity variations in the non‑aqueous phases. If a viscosity correction for brine or high solute concentrations is required, it can be introduced by extending the aqueous viscosity model or by leveraging dedicated brine property options elsewhere in TOUGH4.

For energy conservation, ECOF uses the standard thermodynamic relationship between internal energy and enthalpy. After the TOUGH4 routine provides the pure liquid‑water internal energy, the aqueous molar enthalpy is computed as:

&#x20;                                                                                                             (2-30)                   &#x20;

where u<sub>w</sub> is the molar internal energy of pure liquid water and  is the corrected aqueous molar density including the effects of dissolved tracers and, when applicable, dissolved CO₂. In other words, dissolved components affect h<sub>aq</sub> through the flow‑work term P/ρ, while the internal‑energy term is taken from pure water. This approximation is consistent with treating dissolved components as dilute with respect to aqueous energy storage, while still capturing the first‑order effect of dissolved components on aqueous density and therefore on the enthalpy used in the energy flux and accumulation terms.

TOUGH4 provides an option to include a gravitational potential contribution in the enthalpy variable used internally. In ECOF, when this option is active (MOP2(12) ≠ 0), an additional term proportional to elevation is added to the aqueous enthalpy after the above calculation, following the standard TOUGH4 convention.

2.5  Selection of primary variables.

Table 2-2 summarizes the primary variables used by ECOF under different phase-state conditions. In total, seven distinct phase combinations can be simulated. The number of primary variables is determined by the number of hydrocarbon components and the number of tracer components included in the simulation, and is given by

&#x20;\
<br>

where is the number of hydrocarbon components and is the number of tracers.

Temperature is always included in the ECOF formulation, regardless of whether the simulation is isothermal or non-isothermal. In non-isothermal simulations, temperature is treated as an additional primary variable and is solved as part of the coupled system. In isothermal simulations, temperature is still required for evaluating thermophysical properties, but it is prescribed and remains constant in time; it is therefore not solved as an independent primary variable

_Table 2-2 Primary variables at different phase state conditions_

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Phase Conditions</td><td valign="top">PV_1</td><td valign="top">PV_2</td><td valign="top">PV_3</td><td valign="top">…</td><td valign="top">PV_1+nHC</td><td valign="top">PV_2+nHC</td><td valign="top">…</td><td valign="top">PV_1+nHC+nTR</td><td valign="top">PV_2+nHC+nTR</td></tr><tr><td valign="top">Gas</td><td valign="top">Pg</td><td valign="top">xg<sub>W</sub></td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Aqueous</td><td valign="top">Pa</td><td valign="top">xa<sub>W</sub></td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Oil</td><td valign="top">Po</td><td valign="top">xo<sub>W</sub></td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Aqueous-Gas</td><td valign="top">Pg</td><td valign="top">Sa</td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Oil-Gas</td><td valign="top">Pg</td><td valign="top">xgo<sub>W</sub></td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Aqueous-Oil</td><td valign="top">Po</td><td valign="top">Sa</td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr><tr><td valign="top">Three-phase</td><td valign="top">Pg</td><td valign="top">Sa</td><td valign="top">z<sub>2</sub></td><td valign="top">…</td><td valign="top">z<sub>nHC</sub></td><td valign="top">x<sub>tr1</sub></td><td valign="top">…</td><td valign="top">x<sub>trn</sub></td><td valign="top">T</td></tr></tbody></table>

&#x20;

The first and last primary variables are always pressure and temperature, respectively. The second primary variable represents the water content and is defined either as a water mole fraction or as aqueous saturation, depending on the phase state. Specifically, the water variable may be expressed as the water mole fraction in the gas phase ( ), aqueous phase ( ), or oil phase ( ), or as the total water mole fraction in the combined gas–oil system ( ). In two/three-phase conditions, the water variable is instead represented by the aqueous saturation ( ).

The remaining compositional primary variables correspond to hydrocarbons and tracers. The third through -th primary variables ( – ) are the total mole fractions of hydrocarbon components 2 through , respectively. The final set of primary variables, – , represent the mole fractions of tracer components, defined in a user-specified reference phase.

2.6  Solubility models.

2.8.1 Water solubility in gas or oil phase

ECOF treats H₂O as a full component that can be present in all phases. A key design feature of ECOF is that the hydrocarbon composition variables are defined on a water‑free ("dry") basis, and the water content is represented by a dedicated primary variable whose definition depends on the phase state. Consequently, the algorithm used to determine water mole fractions in gas and oil phase depends on whether water is a primary variable in the existing non‑aqueous phase, whether an aqueous phase is present (in which case non‑aqueous phases are treated as water‑saturated), or whether the system is in the oil+gas two‑phase region without an aqueous phase (where only the total water content of the combined gas–oil system is known).

In the single‑phase gas state, the water mole fraction in the gas phase is itself a primary variable and is read directly from the second primary variable. A condensation check is applied in this state: the code evaluates the water partial pressure ps and compares it with the saturation vapor pressure psat. If ps > psat, an aqueous phase is thermodynamically required, and the element is switched from the gas‑only state to the aqueous+gas state.

In the single‑phase oil state, the oil‑phase water mole fraction is likewise a primary variable, and ECOF sets water mole fraction in oil phase with the second primary variable after enforcing it being larger than 0. To ensure physical consistency, ECOF computes the water solubility limit in oil. If calculated water mole fraction is larger than the water solubility limit, the oil can no longer dissolve all the water, and an aqueous phase must form; in that case the element is switched from the oil‑only state to the aqueous+oil state.

When an aqueous phase exists, ECOF treats the non‑aqueous phases as being in equilibrium with liquid water. Accordingly, water in the gas phase is determined from the saturation vapor pressure, while water in the oil phase is set to the oil‑phase solubility limit.

For the gas phase, ECOF computes psat(T) and assigns:

,   if psat ≤ P;  otherwise  1.0                                                        (2-31)

For the oil phase, the equilibrium mole fraction of water in the oil phase is controlled by the temperature-dependent solubility (Hoot, et. al, 1957) adjusted by the pressure:

&#x20;                                                                                  (2-32)                         &#x20;

where _P_<sub>_0_</sub> (= 1 atm) is the reference pressure.

In the oil+gas two‑phase state without an aqueous phase, ECOF does not prescribe separate water mole fractions in the gas and oil phases. Instead, the second primary variable represents the total water content of the combined gas–oil system on the same dry basis used for the hydrocarbon composition variables. The hydrocarbon phase split is obtained first by a PR‑EOS flash calculation for the hydrocarbon subsystem (excluding water), which returns the hydrocarbon vapor fraction β (variable beta in the code) and the corresponding dry hydrocarbon compositions xc(i) (oil) and yc(i) (gas).

Before partitioning water between oil and gas, ECOF applies a screening check for possible aqueous‑phase appearance. Using the water saturation pressure psat(T), the code tests whether the (approximate) water partial pressure exceeds psat(T) by a small margin (2×10³ Pa). If so, the element is switched to the three‑phase state.

If no aqueous phase is triggered, ECOF partitions the total water between oil and gas using the oil solubility limit  and the hydrocarbon vapor fraction β. The first step is to compute the maximum amount of water that can be dissolved in the oil phase if the oil is saturated and the gas contains no water. In the implementation this quantity is:

&#x20;                                                                                          (2-33)

If the specified total water content (xgo<sub>W</sub>, from primary variable) exceeds this oil capacity  (xgo<sub>W</sub> > ), the oil phase is set to its solubility limit and the excess water is assigned to the gas phase. The code computes:

&#x20; &#x20;

&#x20;&#x20;

&#x20;                                                                                        (2-34)

If the specified total water content is below the oil capacity, ECOF assumes that all water is dissolved in the oil phase and the gas phase contains no water.

The effects of H2O in either the gas phase or the oil phase on the partitioning coefficient (_K_-value) of HC components between non-aqueous phases are negligible.

2.8.2 Hydrocarbon/Gas solubility in aqueous phase

ECOF represents dissolution of gaseous components (and, in a limited way, hydrocarbon components) in the aqueous phase using a Henry’s-law equilibrium relation between the aqueous phase and a coexisting non‑aqueous phase. This approach is robust for key gas components for which Henry constants (or equivalent solution equilibrium constants) are available, but it is not a complete aqueous-solubility model for arbitrary multi‑component oils.

For a component _i_ in equilibrium between a gas phase and the aqueous phase, ECOF adopts the Henry’s-law form

&#x20;                                                                                                                     (2-35)

where _P_<sub>_i_</sub> is the component partial pressure in the gas phase, _H_<sub>_i_</sub> is the Henry constant (Pa), and _x_<sub>_i,a_</sub> is the aqueous‑phase mole fraction of component _i_. Writing , with  the gas‑phase mole fraction and _P_ the total gas pressure, the dissolved mole fraction is obtained as

&#x20;                                                                                                                     (2-36)

In ECOF this is implemented directly for hydrocarbon/gas components. When an oil phase coexists with the aqueous phase, but no gas phase exists, ECOF uses the same functional form with the oil‑phase composition as a proxy. This is a pragmatic approximation and should be regarded as reliable mainly for light/volatile components; aqueous solubility of heavier oil pseudo‑components is generally neglected or poorly constrained.

Henry constants are provided only for a limited set of components. TOUGH4 provides a function which contains temperature-dependent correlations (Cramer,1982; and D’Amore and Truesdell 1988) for selected gases (e.g., CH4, C2H6, C3H8, H2S, CO2, N2, O2, H2, and light C4 species). For components without a correlation, the function returns a very large value (_H_<sub>_i_</sub> ≈ 1×10^50 Pa).  The calculated Henry constant will be used as an initial guess for further computation of an “effective Henry constant” based on local thermodynamic equilibrium as described by Oldenburg et al. (2004). In this approach, partitioning of the gas components between the gaseous and aqueous phases is calculated using an accurate effective Henry’s coefficient.

This approach uses the cubic EOS solutions to compute gas‑phase fugacity coefficients and then obtain solution equilibrium constants logk(i). For each supported component, the effective Henry constant is evaluated as

&#x20;                                                                          (2-37)

where  is the fugacity coefficient and 55.508 is the molar concentration of water (kg/mol) used to convert from molality-based equilibrium constants to a mole‑fraction-based Henry form. If logk(i) is unavailable (returned as zero), lets  Pa.

Because gas fugacity coefficients ( ) depend on gas composition, ECOF includes an iterative helper routine that updates Henry constants through repeated calls to the routines for cubic EOS and computes the effective Henry constant. In each iteration, provisional gas-phase mole fractions are computed from   (and ), then fugacity coefficients and solution equilibrium constants are updated and  is recomputed until the relative change in  falls below a small tolerance or a maximum number of iterations is reached.

The current TOUGH4/ECOF implementation provides a numerically robust mechanism for representing dissolution/exsolution of a subset of gases (notably CO2, H2S, CH4, N2, etc.) in the aqueous phase. However, it does not constitute a general aqueous solubility model for multicomponent oils: components without Henry/solution data are treated as effectively insoluble, and oil–water partitioning is approximated using a Henry-type relation when no gas phase exists. For applications where aqueous solubility of oil components is important, additional correlations or coupling to more detailed geochemical/solubility models are required.

2.7  Saturation calculation

ECOF supports seven phase-state combinations: gas only (G), aqueous only (A), oil only (O), gas+aqueous (G+A), gas+oil (G+O), aqueous+oil (A+O), and gas+aqueous+oil (G+A+O). The saturations are determined based on the phase state condition. They either are primary variables or can be calculated from primary variables.

For single-phase states, saturations are prescribed directly (independent of composition):

&#x20; • G:  Sg = 1, Sa = 0, So = 0.

&#x20; • A: Sa = 1, Sg = 0, So = 0.

&#x20; • O: So = 1, Sg = 0, Sa = 0.

For two-phase states that include the aqueous phase (G+A and A+O), the aqueous saturation Sa is the second primary variable. The complementary saturation is computed by closure:

&#x20; • G+A:  Sg = 1 − Sa, So = 0.

&#x20; • A+O:  So = 1 − Sa, Sg = 0.

For the G+O state, neither phase saturation is a primary variable. Instead, ECOF converts the hydrocarbon flash “vapor fraction” β (molar fraction of hydrocarbons in the gas phase) to volumetric phase fractions using phase molar densities. Let _dgas_ and _doil_ denote the molar densities (mol·m⁻³) of the gas and oil phases, computed from the Peng–Robinson EOS routines. For a total hydrocarbon mole inventory _nHC_, the phase volumes are proportional to

Vg ∝ (β · nHC)/dgas,     Vo ∝ ((1 − β) · nHC)/doil.

Therefore, the gas saturation is computed as the gas volume fraction of the combined (gas+oil) pore space:

&#x20;                                                                                                                 (2-38)

So = 1 − Sg,     Sa = 0.

For the three-phase state (G+A+O), Sa is again a primary variable. The remaining pore volume (1 − Sa) is occupied by the non-aqueous phases (gas+oil). ECOF distributes this non-aqueous volume between gas and oil using a volumetric gas fraction .  is derived from the hydrocarbon flash vapor fraction β together with the phase molar densities _dgas_ and _doil_.

Because the PR flash is performed on the hydrocarbon subsystem (NumHyC components), while a small amount of H2O may also be present in the gas (water vapor) and in the oil (dissolved water), ECOF applies a conversion factor to map hydrocarbon moles to total phase moles. In the current implementation, the correction is applied via

&#x20;αG = 1/(1-xgw),     αL = 1/(1–xow)

where xgw = psat(T)/P is the gas-phase water mole fraction and xow is the oil-phase water mole fraction at saturation. Using these factors,  is computed as

&#x20;                                                                                                          (2-39)                    &#x20;

Finally, saturations are

Sg = (1 − Sa) · ,     So = 1 − Sa − Sg.

This approach yields an exact conversion from hydrocarbon moles to total phase moles when water is treated as a true additional component.

&#x20;     2.10  Logic of phase switching

Phase switching in ECOF is implemented by validating the currently assumed phase state and, when a boundary is crossed, changing immediately to the new phase state. To keep the Newton iteration and Jacobian assembly stable, switching is only allowed during the main evaluation (ishift = 0) and when the element is not already flagged as “recently switched” (ElemState(n)%changes = 0). After a switch, ElemState(n)%changes is set to a positive code value, and a delay mechanism increments this counter until it exceeds IE(64), after which it is reset to zero. This introduces a short “phase persistence” interval that suppresses rapid toggling.

2.10.1 Hydrocarbon flash–based switching

Hydrocarbon phase appearance/disappearance is governed by the compositional PR flash calculation. ECOF interprets the returned phase\_flag from flash as:

&#x20; • phase\_flag = 1: single vapor phase (G).

&#x20; • phase\_flag = 2: single liquid phase (O).

&#x20; • phase\_flag = 3: two-phase split (G + O).

Accordingly, switching among G, O, and G+O proceeds as:

&#x20; • In G: a flash is performed using the current overall hydrocarbon composition. If phase\_flag=3, oil appears and the element switches to G+O condition (G → G+O).

&#x20; • In O: a flash is performed with a liquid initial guess. If phase\_flag=3, gas appears and the element switches to G+O condition (O → G+O).

&#x20; • In G+O: a flash is repeated. If phase\_flag=1, the oil phase disappears and the element switches to G condition (G+O → G). If phase\_flag=2, the gas phase disappears and the element switches to O condition (G+O → O).

2.10.2 Water-driven switching involving the aqueous phase

Transitions that create or remove the aqueous phase are driven by water vapor-pressure constraints and dissolved-water limits:

&#x20; • Gas → Aqu+Gas: In G conditon, the water partial pressure is Pw = xgw·P. If Pw exceeds the saturation vapor pressure psat(T), an aqueous phase is created.

&#x20; • Oil → Aqu+Oil: In O condition, if the dissolved water mole fraction in oil exceeds the solubility limit xow > solwat\_oil(T,P), an aqueous phase is created.

&#x20; • Gas+Oil → Three phases: In G+O condition, ECOF checks whether the total water content carried by the gas+oil system can be kept as vapor/dissolved water. A practical condensation criterion is used: if water partial pressure exceeds psat(T) + 2000 Pa, an aqueous phase is created.

&#x20; • Two-phase → single-phase by saturation closure: In A+G and A+O condition, disappearance of one phase is handled by saturation thresholds: if Sa ≤ 0 the aqueous phase disappears (Aqu+Gas → Gas, Aqu+Oil → Oil). If the complementary saturation Sg ≤ 0 (Aqu+Gas) or So ≤ 0 (Aqu+Oil), the non-aqueous phase disappears (Aqu+Gas → Aqu, Aqu+Oil → Aqu).

&#x20; • Three phases → Gas+Oil: In three-phase condition, if Sa ≤ 0 the aqueous phase disappears and the state switches to G+O condition.

2.10.3 Switching between two-phase and three-phase states

When an aqueous phase exists, the PR flash is used to determine whether the hydrocarbon subsystem is single-phase or splits into gas+oil. This provides the main trigger between (Aqu+Gas), (Aqu+Oil), and (Gas+Aqu+Oil):

&#x20; • Aqu+Gas → Three phases: In G+A condition, if a hydrocarbon flash returns phase\_flag=3, an oil phase is predicted to coexist with the gas. The element switches to three-phase condition (Aqu+Gas → Three phases).

&#x20; • Aqu+Oil → Three phases: In  O+A condition, if a hydrocarbon flash indicates two-phase conditions, ECOF enables a robust gas-appearance gate to prevent spurious “micro-gas.” The gate requires strong evidence of two-phase behavior (based on the K-value stability functions f0 and f1) and/or that the computed β exceeds a micro-phase cutoff (β > 10⁻¹⁰ when phase\_flag=3). The evidence must persist for two consecutive evaluations (phase sticky count = 2) before switching to three-phase condition.

&#x20; • Three phases → Aqu+Oil (gas disappearance): ECOF uses a complementary robust gate for gas disappearance. A switch to O+A condition is only allowed when the hydrocarbon flash indicates a single-liquid solution (phase\_flag=2), both stability indicators are strongly negative (f0 and f1 below small offsets), and the computed β is extremely small (β < 10⁻¹⁰). This condition must persist for four consecutive evaluations (phase sticky count = 4) before switching.

&#x20; • Three phases → Aqu+Gas (oil disappearance): When the flash indicates a single-vapor hydrocarbon solution (phase\_flag=1), ECOF may switch to G+A condition. In the current implementation an additional heuristic uses the current oil saturation So < 0.2 as a permissive condition for declaring oil disappearance.

2.10.4 Numerical robustness considerations

ECOF includes several safeguards to reduce oscillatory phase switching (“chattering”) and to avoid creating numerically problematic micro-phases. First, switching is disabled during derivative evaluations (ishift ≠ 0) and for a short persistence interval after each switch. Second, water-driven transitions include small safety margins (e.g., using pgas > 1.01·P for exsolution and xogw·P > psat(T)+2000 Pa for condensation). Third, micro-phase cutoffs and stability function thresholds are applied in A+O condition and three-phase condition: β is compared to 10⁻¹⁰ and stability indicators f0 and f1 must exceed small offsets before a new phase is admitted or removed. Finally, “sticky counters” require the same switching condition to be satisfied for multiple consecutive evaluations (2 or 4 counts depending on the direction) before the phase state is updated.
