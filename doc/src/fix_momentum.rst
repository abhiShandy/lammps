.. index:: fix momentum

fix momentum command
====================

fix momentum/kk command
=======================

Syntax
""""""

.. parsed-literal::

   fix ID group-ID momentum N keyword values ...

* ID, group-ID are documented in :doc:`fix <fix>` command
* momentum = style name of this fix command
* N = adjust the momentum every this many timesteps
  one or more keyword/value pairs may be appended
* keyword = *linear* or *angular* or *rescale*

  .. parsed-literal::

       *linear* values = xflag yflag zflag
         xflag,yflag,zflag = 0/1 to exclude/include each dimension
       *angular* values = none

  .. parsed-literal::

       *rescale* values = none

Examples
""""""""

.. code-block:: LAMMPS

   fix 1 all momentum 1 linear 1 1 0
   fix 1 all momentum 1 linear 1 1 1 rescale
   fix 1 all momentum 100 linear 1 1 1 angular

Description
"""""""""""

Zero the linear and/or angular momentum of the group of atoms every N
timesteps by adjusting the velocities of the atoms.  One (or both) of
the *linear* or *angular* keywords must be specified.

If the *linear* keyword is used, the linear momentum is zeroed by
subtracting the center-of-mass velocity of the group from each atom.
This does not change the relative velocity of any pair of atoms.  One
or more dimensions can be excluded from this operation by setting the
corresponding flag to 0.

If the *angular* keyword is used, the angular momentum is zeroed by
subtracting a rotational component from each atom.

This command can be used to insure the entire collection of atoms (or
a subset of them) does not drift or rotate during the simulation due
to random perturbations (e.g. :doc:`fix langevin <fix_langevin>`
thermostatting).

The *rescale* keyword enables conserving the kinetic energy of the group
of atoms by rescaling the velocities after the momentum was removed.

Note that the :doc:`velocity <velocity>` command can be used to create
initial velocities with zero aggregate linear and/or angular momentum.

----------

.. include:: accel_styles.rst

**Restart, fix_modify, output, run start/stop, minimize info:**

No information about this fix is written to :doc:`binary restart files <restart>`.  None of the :doc:`fix_modify <fix_modify>` options
are relevant to this fix.  No global or per-atom quantities are stored
by this fix for access by various :doc:`output commands <Howto_output>`.
No parameter of this fix can be used with the *start/stop* keywords of
the :doc:`run <run>` command.  This fix is not invoked during :doc:`energy minimization <minimize>`.

Restrictions
""""""""""""
 none

Related commands
""""""""""""""""

:doc:`fix recenter <fix_recenter>`, :doc:`velocity <velocity>`

**Default:** none
