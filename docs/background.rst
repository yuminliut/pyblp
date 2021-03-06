Background
==========

The following sections provide a brief overview of the BLP model and how it is estimated.


The Model
---------

At a high level, there are :math:`t = 1, 2, \dotsc, T` markets, each with :math:`j = 1, 2, \dotsc, J_t` products produced by :math:`f = 1, 2, \dotsc, F_t` firms. There are :math:`i = 1, 2, \dotsc, I_t` agents who choose among the :math:`J_t` products and an outside good, denoted by :math:`j = 0`. The set :math:`\mathscr{J}_{ft} \subset \{1, 2, \ldots, J_t\}` denotes the products produced by firm :math:`f` in market :math:`t`.


Demand-Side
~~~~~~~~~~~

Observed demand-side product characteristics are contained in the :math:`N \times K_1` matrix of linear characteristics, :math:`X_1`, and the :math:`N \times K_2` matrix of nonlinear characteristics, :math:`X_2`. Characteristic columns can overlap. For example, either matrix may contain a constant column, and :math:`X_2` often contains a column of prices that always exists in :math:`X_1`. Unobserved demand-side product characteristics, :math:`\xi`, are a :math:`N \times 1` column vector.

In market :math:`t`, observed agent characteristics are a :math:`I_t \times D` matrix called demographics, :math:`d`. Note that in :ref:`Nevo (2000) <n00>`, :math:`d` refers to the number of demographics and :math:`D` to the matrix; the opposite is employed here so that all numbers are capital letters. Unobserved characteristics are a :math:`I_t \times K_2` matrix, :math:`\nu`, which has rows that are usually assumed to be IID draws from a mean-zero multivariate normal distribution.

The indirect utility of agent :math:`i` from consuming product :math:`j` in market :math:`t` is

.. math:: U_{jti} = \delta_{jt} + \mu_{jti} + \epsilon_{jti},
   :label: utilities

in which the mean utility for products is

.. math:: \delta = X_1\beta + \xi,

and the type-specific portion for all products and agents in a single market is

.. math:: \mu = X_2(\Sigma\nu' + \Pi d').

Unconventionally, the linear coefficient on price, :math:`-\alpha`, is the first element in the :math:`K_1 \times 1` column vector :math:`\beta`. Accordingly, prices, :math:`p`, are the first column in :math:`X_1`. If prices enter utility nonlinearly, then :math:`p` will also be the first column in :math:`X_2`, and the nonlinear coefficient on price, :math:`-\alpha_i`, will be the first element in :math:`\Sigma\nu_i + \Pi d_i`.

The :math:`K_2 \times K_2` matrix :math:`\Sigma` is the Cholesky decomposition of the covariance matrix that defines the multivariate normal distribution from which each :math:`\nu_i` is assumed to be drawn. The :math:`K_2 \times D` matrix :math:`\Pi` measures how agent tastes vary with demographics.

Random idiosyncratic preferences :math:`\epsilon_{jti}` are assumed to be Type I Extreme Value so that market shares can be approximated with Monte Carlo integration or quadrature rules as in :ref:`Heiss and Winschel (2008) <hw08>` and :ref:`Skrainka and Judd (2011) <sj11>`:

.. math:: s_{jt} = \sum_{i=1}^{I_t} w_i s_{jti}(\nu_i) = \sum_{i=1}^{I_t} w_i\,\frac{\exp(\delta_{jt} + \mu_{jti})}{1 + \sum_{k=1}^{J_t} \exp(\delta_{kt} + \mu_{kti})},
   :label: shares

in which :math:`s_{jti}` is the probability that agent :math:`i` chooses product :math:`j` in market :math:`t`, :math:`w` is a :math:`I_t \times 1` column vector of integration weights, and :math:`\nu_i` consists of the :math:`K_2` integration nodes associated with :math:`w_i`.


Supply-Side
~~~~~~~~~~~

Observed supply-side product characteristics are the :math:`N \times K_3` matrix of cost characteristics, :math:`X_3`. Prices cannot be cost characteristics, but non-price product characteristics often overlap with the demand-side characteristics in :math:`X_1` and :math:`X_2`. Unobserved supply-side product characteristics, :math:`\omega`, are a :math:`N \times 1` column vector. Note that in contrast to :ref:`Berry, Levinsohn, and Pakes (1995) <blp95>`, the notation for observed cost characteristics is similar to the notation for demand-side characteristics.

Firms play a differentiated Bertrand-Nash pricing game. Firm :math:`f` produces a subset of the :math:`J_t` products in market :math:`t` and chooses prices to maximize the sum of population-normalized gross expected profits, which for product :math:`j` in market :math:`t` are

.. math:: \pi_{jt} = (p_{jt} - c_{jt})s_{jt},

in which marginal costs for all products are defined according either to a linear or a log-linear specification:

.. math:: \tilde{c} = X_3\gamma + \omega \quad\text{where}\quad \tilde{c} = c \quad\text{or}\quad \tilde{c} = \log c.
   :label: costs

The :math:`K_3 \times 1` column vector :math:`\gamma` measures how marginal costs vary with cost characteristics. Regardless of how marginal costs are specified, the first-order conditions of firms in a market can be rewritten after suppressing market subscripts as

.. math:: p = c + \eta.
   :label: eta_markup

Called the BLP-markup equation in :ref:`Morrow and Skerlos (2011) <ms11>`, the markup term is

.. math:: \eta = -(O \circ \frac{\partial s}{\partial p})^{-1}s,
   :label: eta

in which the market's owenership matrix, :math:`O`, is definited in terms of its corresponding cooperation matrix, :math:`\kappa`, by :math:`O_{jk} = \kappa_{fg}` where :math:`j \in \mathscr{J}_{ft}`, the set of products produced by firm :math:`f` in the market, and similarly, :math:`g \in \mathscr{J}_{gt}`. Usually, :math:`\kappa = I`, the identity matrix, so :math:`O_{jk}` is simply :math:`1` if the same firm produces products :math:`j` and :math:`k`, and is :math:`0` otherwise.

The Jacobian in the BLP-markup equation can be decomposed into

.. math:: \frac{\partial s}{\partial p} = \Lambda - \Gamma,

in which :math:`\Lambda` is a diagonal :math:`J_t \times J_t` matrix that can be approximated by

.. math:: \Lambda_{jj} = \sum_{i=1}^{I_t} w_i s_{jti}\frac{\partial U_{jti}}{\partial p_{jt}}
   :label: capital_lambda

and :math:`\Gamma` is another :math:`J_t \times J_t` matrix that can be approximated by

.. math:: \Gamma_{jk} = \sum_{i=1}^{I_t} w_i s_{jti}s_{kti}\frac{\partial U_{jti}}{\partial p_{jt}}.
   :label: capital_gamma

Derivatives in these expressions are derived from the definition of :math:`U` in :eq:`utilities`. An alternative way to write the first-order conditions is with what :ref:`Morrow and Skerlos (2011) <ms11>` call the :math:`\zeta`-markup equation,

.. math:: p = c + \zeta,
   :label: zeta_markup

in which the markup term is

.. math:: \zeta = \Lambda^{-1}(O \circ \Gamma)'(p - c) - \Lambda^{-1}.
   :label: zeta


Identification
~~~~~~~~~~~~~~

The unobserved product characteristics can be stacked to form the combined error term,

.. math:: u = \begin{bmatrix} \xi \\ \omega \end{bmatrix},

and similarly, :math:`Z_D` and :math:`Z_S`, which are :math:`N \times M_D` and :math:`N \times M_S` matrices of demand- and supply-side instruments, can be stacked to form the combined block-diagonal matrix of instruments,

.. math:: Z = \begin{bmatrix} Z_D & 0 \\ 0 & Z_S \end{bmatrix}.

The GMM moment conditions are

.. math:: \mathrm{E}[g_i] = 0 \quad\text{where}\quad g_i = u_iZ_i.
   :label: moments

Demand-side instruments include all non-price product characteristics from :math:`X_1` and :math:`X_2`, and supply-side instruments include :math:`X_3`. Since cost characteristics are often good demand-side instruments and vice versa, both :math:`Z_D` and :math:`Z_S` often include all characteristics.


Estimation
----------

There are four sets of parameters to be estimated: :math:`\beta`, :math:`\Sigma`, :math:`\Pi`, and :math:`\gamma`. If the supply side is not considered, only the first three sets of parameters are estimated. The linear parameters, :math:`\beta` and :math:`\gamma`, are concentrated out of the problem. Unknown elements in the remaining matrices of nonlinear parameter, :math:`\Sigma` and :math:`\Pi`, are collectively referred to as :math:`\theta`, a :math:`P \times 1` column vector. If demographics are not included, :math:`\theta` will only consist of elements from :math:`\Sigma`.

The GMM problem is

.. math:: \min_\theta u'ZWZ'u,
   :label: objective

in which :math:`W` is a combined block-diagonal weighting matrix that consists of separate demand- and supply-side weighting matrices,

.. math:: W = \begin{bmatrix} W_D & 0 \\ 0 & W_S \end{bmatrix},

which is assumed to have an inverse that is a consistant estimate of :math:`\mathrm{E}[Z'uu'Z]`.

If only the demand side is estimated, :math:`u = \xi`, :math:`Z = Z_D`, and :math:`W = W_D`.

Conventionally, the 2SLS weighting matrix, :math:`W = (Z'Z)^{-1}`, is used in the first stage. With two-step or iterated GMM, the weighting matrix is updated before each subsequent stage according to :math:`W = (g'g)^{-1}`. Before entering into this expression, the sample moments are often centered.

In each stage, a nonlinear optimizer is used to find values of :math:`\hat{\theta}` that minimize the GMM objective. The gradient of the objective is typically computed to speed up optimization.


The Objective
~~~~~~~~~~~~~

Given a :math:`\hat{\theta}`, the first step towards computing its associated objective value is computing :math:`\delta(\hat{\theta})` in each market with the following standard contraction:

.. math:: \delta \leftarrow \delta + \log s - \log s(\delta, \hat{\theta})

where :math:`s` are the market's observed shares and :math:`s(\hat{\theta}, \delta)` are shares evaluated at :math:`\hat{\theta}` and the current iteration's :math:`\delta`. As noted in the appendix of :ref:`Nevo (2000) <n00>`, exponentiating both sides of the contraction mapping and iterating over :math:`\exp(\delta)` gives an alternate formulation that can be faster. Conventional starting values are those that solve the logit model, :math:`\delta_{jt} = \log s_{jt} - \log s_{0t}`.

The mean utility in conjunction with the demand-side conditional independence assumption in :eq:`moments` is used to recover the demand-side linear parameters with

.. math:: \hat{\beta} = (X_1'Z_DW_DZ_D'X_1)^{-1}X_1'Z_DW_DZ_D'\delta(\hat{\theta}).

The demand-side linear parameters are in turn are used to recover the unobserved demand-side product characteristics,

.. math:: \xi(\hat{\theta}) = \delta(\hat{\theta}) - X_1\hat{\beta}.

If the supply side is considered, the BLP-markup equation from :eq:`eta_markup` is employed to compute marginal costs,

.. math:: c(\hat{\theta}) = p - \eta(\hat{\beta}, \hat{\theta}),

and in conjunction with the supply-side conditional independence assumption in :eq:`moments`, marginal costs are used to recover the supply-side linear parameters according to their specification in :eq:`costs` with

.. math:: \hat{\gamma} = (X_3'Z_SW_SZ_S'X_3)^{-1}X_3'Z_SW_SZ_S'\tilde{c}(\hat{\theta}).

The supply-side linear parameters are in turn are used to recover the unobserved supply-side product characteristics,

.. math:: \omega(\hat{\theta}) = \tilde{c}(\hat{\theta}) - X_3\hat{\gamma}.

Finally, interacting the estimated unobserved product characteristics with the instruments gives the GMM objective value in :eq:`objective`.


The Gradient
~~~~~~~~~~~~

The gradient of the GMM objective in :eq:`objective` is

.. math:: 2\left(\frac{\partial u}{\partial\theta}\right)'ZWZ'u,

in which Jacobians of the unobserved product characteristics are stacked to form

.. math:: \frac{\partial u}{\partial\theta} = \begin{bmatrix} \frac{\partial\xi}{\partial\theta} \\ \frac{\partial\omega}{\partial\theta} \end{bmatrix} = \begin{bmatrix} \frac{\partial\delta}{\partial\theta} \\ \frac{\partial\tilde{c}}{\partial\theta} \end{bmatrix}.

The demand-side Jacobian can be computed by writing :math:`\delta` as an implicit function of :math:`s`:

.. math:: \frac{\partial\delta}{\partial\theta} = -\left(\frac{\partial s}{\partial\delta}\right)^{-1}\frac{\partial s}{\partial\theta}.

Derivatives in this expression are derived directly from the definition of :math:`s` in :eq:`shares`.

The supply-side Jacobian can be derived from the BLP-markup equation in :eq:`eta_markup`:

.. math:: \frac{\partial\tilde{c}}{\partial\theta_p} = -\frac{\partial\tilde{c}}{\partial c}\frac{\partial\eta}{\partial\theta}.

The first term in this expression depends on whether marginal costs are defined according either to a linear or a log-linear specification, and the second term is derived from the definition of :math:`\eta` in :eq:`eta`. Specifically, letting :math:`A = O \circ (\Gamma - \Lambda)`,

.. math:: \frac{\partial\eta}{\partial\theta} = -A^{-1}\left(\frac{\partial A}{\partial\theta}\eta + \frac{\partial A}{\partial\xi}\eta\frac{\partial\xi}{\partial\theta}\right),

in which

.. math:: \frac{\partial A}{\partial\theta} = O \circ \left(\frac{\partial\Gamma}{\partial\theta} - \frac{\partial\Lambda}{\partial\theta}\right) \quad\text{and}\quad \frac{\partial A}{\partial\xi} = O \circ \left(\frac{\partial\Gamma}{\partial\xi} - \frac{\partial\Lambda}{\partial\xi}\right)

are derived from the definitions of :math:`\Gamma` and :math:`\Lambda` in :eq:`capital_gamma` and :eq:`capital_lambda`.


Standard Errors
~~~~~~~~~~~~~~~

Computing standard errors requires the Jacobian of the moments with respect to :math:`\theta`, :math:`\beta`, and :math:`\gamma`, which is

.. math:: G = Z' \begin{bmatrix} \frac{\partial\xi}{\partial\theta} & X_1 & 0 \\ \frac{\partial\omega}{\partial\theta} & 0 & X_3 \end{bmatrix}.

Before updating the weighting matrix, standard errors are extracted from an estimate of

.. math:: \text{Var}\begin{pmatrix} \hat{\theta} \\ \hat{\beta} \\ \hat{\gamma} \end{pmatrix} = (G'WG)^{-1}G'WSWG(G'WG)^{-1},

in which

.. math:: S = Z' \begin{bmatrix} u_1^2 && 0 \\ & \ddots & \\ 0 && u_N^2 \end{bmatrix} Z.

These standard errors are called robust. If the weighting matrix was chosen such that :math:`W = S^{-1}`, then

.. math:: \text{Var}\begin{pmatrix} \hat{\theta} \\ \hat{\beta} \\ \hat{\gamma} \end{pmatrix} = (G'WG)^{-1}.

The standard errors extracted from an estimate of this last expression are called unadjusted.


Bertrand-Nash Prices and Shares
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Computing equilibrium prices and shares is necessary during post-estimation to evaluate counterfactuals such as mergers. Similarly, synthetic data can be simulated in a straightforward manner according to a demand-side specification, but if the data are to simultaneously conform to a supply-side specification as well, it is necessary to compute equilibrium prices and shares that are implied by the other synthetic data.

To efficiently compute equilibrium prices, the :math:`\zeta`-markup equation from :ref:`Morrow and Skerlos (2011) <ms11>` in :eq:`zeta_markup` is employed in the following contraction:

.. math:: p \leftarrow c + \zeta(p).

When computing :math:`\zeta(p)`, shares :math:`s(p)` associated with the candidate equilibrium prices are computed according to their definition in :eq:`shares`.

Of course, marginal costs, :math:`c`, are required to iterate over the contraction. When evaluating counterfactuals, costs are usually computed first according to the BLP-markup equation in :eq:`eta_markup`. When simulating synthetic data, marginal costs are simulated according their specification in :eq:`costs`.
