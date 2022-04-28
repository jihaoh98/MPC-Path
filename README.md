# MPC Path
## Experimental result
> set the Delay in ./src/car_simulator/config/car_simulator.yaml for zero.
<p align="center">
    <img src="mpc.gif" width="400"/>
</p>

## Convert the form of J to the form of QP
>$$
J = min_U \quad (X-X_{ref})^{T}Q(X-X_{ref}) \\
X = BB * U + AA * x_{0} + gg  \\
X-X_{ref} = BB * U + AA * x_{0} + gg - X_{ref}  \qquad set \quad AA * x_{0} - X_{ref} \quad as \quad E \\
X-X_{ref} = BB * U + E + gg
$$


Expand the formula:(only optimize the variable related to U)
>$$
J = (E + BB * U + gg)^{T}Q(E + BB * U + gg)  \\
J = U^{T}BB^{T}QBBU + 2U^{T}BB^{T}QE + 2U^{T}BB^{T}Qgg \\
J = U^{T}BB^{T}QBBU + 2U^{T}BB^{T}Q(AA * x_{0} +gg - X_{ref})
$$

So we can get the $qx$ in code equal to $-Qx * X_{ref}$

## Some core code and explaination



