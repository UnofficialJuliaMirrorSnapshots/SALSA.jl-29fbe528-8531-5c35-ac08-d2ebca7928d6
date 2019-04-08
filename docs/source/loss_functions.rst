Loss Functions
==============

This part of the package provides a description and mathematical background of the implemented loss functions. Every loss function can be supplied to ``salsa`` subroutines either directly (see :func:`salsa`) or passed within ``SALSAModel``. In the definitions below :math:`l(y,p)` stands for the loss loss function evaluated at the true label :math:`y` and a prediction :math:`p`.

.. function:: HINGE
	
	Defines an implementation of the `Hinge Loss <https://en.wikipedia.org/wiki/Hinge_loss>`_ function, *i.e.* :math:`l(y,p) = \max(0,1 - yp)`.
	
.. function:: LOGISTIC

	Defines an implementation of the `Logistic Loss <https://en.wikipedia.org/wiki/Logit>`_ function, *i.e.* :math:`l(y,p) = \log(1 + \exp(-yp))`.
	
.. function:: LEAST_SQUARES

	Defines an implementation of the `Least Squares Loss <https://en.wikipedia.org/wiki/Mean_squared_error>`_ function, *i.e.* :math:`l(y,p) = \frac{1}{2}(p - y)^2`.
	
.. function:: SQUARED_HINGE

	Defines an implementation of the Squared Hinge Loss function, *i.e.* :math:`l(y,p) = \max(0,1 - yp)^2`.
	
.. function:: PINBALL

	Defines an implementation of the `Pinball (Quantile) Loss <http://www.lokad.com/pinball-loss-function-definition>`_ function, *i.e.* 
	
	.. math::
		l(y,p) = \left\lbrace\begin{array}{ll}
				 1 - yp, & \rm{if} \hspace{1mm} yp \leq 1, \\
				 \tau(yp - 1), & \rm{otherwise} \\
				 \end{array}\right.
				 
	If ``PINBALL`` loss is selected :math:`\tau` parameter will be tuned by the build-in cross-validation routines.
				 
.. function:: MODIFIED_HUBER

	Defines an implementation of the `Modified Huber Loss <https://en.wikipedia.org/wiki/Huber_loss>`_ function, *i.e.*
	
	.. math::
		l(y,p) = \left\{\begin{array}{ll} 
				 -4yp, & \rm{if} \hspace{1mm} yp < -1 \\ 
    			 \max(0,1 - yp)^2, & \rm{otherwise} \\
    			 \end{array}\right.
    			 
.. function:: loss_derivative(type)

	Defines a derivative of the loss function. One can pass any type of the loss function, *e.g.* ``HINGE`` or an entire algorithm, for instance :func:`RK_MEANS`.
	
	:param type: type of the loss function, *e.g.* ``HINGE`` or an entire algorithm
	
	:return: ``Function`` which calculates a derivative at the current iterate :math:`w_t`, subsample :math:`\mathcal{A}_t` and label :math:`y_t`