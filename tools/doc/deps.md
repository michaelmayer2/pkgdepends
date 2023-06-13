R packages may have various types of dependencies, see
\href{https://cran.r-project.org/doc/manuals/R-exts.html}{Writing R Extensions}.

pak groups dependencies into three groups:
\itemize{
\item hard dependencies: "Depends", "Imports", and "LinkingTo",
\item soft dependencies: "Suggests" and "Enhances",
\item extra dependencies, see below.
}

pak supports concise ways of specifying which types of
dependencies of a package should be installed.
It is similar to how \code{\link[utils:install.packages]{utils::install.packages()}} interprets its
\code{dependencies} argument.

You typically use one of these values:
\itemize{
\item \code{NA} or \code{"hard"} to install a package and its required dependencies,
\item \code{TRUE} to install all required dependencies, plus optional and development
dependencies.
}

If you need more flexibility, the full description of possible values for
the \code{dependencies} argument are:
\itemize{
\item \code{TRUE}: This means all hard dependencies plus \code{Suggests} for
direct installations, and hard dependencies only for dependent
packages.
\item \code{FALSE}: no dependencies are installed at all.
\item \code{NA} (any atomic type, so \code{NA_character_}, etc. as well): only hard
dependencies are installed.
\item If a list with two entries named \code{direct} and \code{indirect}, it is taken
as the requested dependency types, for direct installations and
dependent packages.
\item If a character vector, then it is taken as the dependency types
for direct installations, and the hard dependencies are
used for the dependent packages.
}

If \code{"hard"} is included in the value or a list element, then it is replaced
by the hard dependency types.
If \code{"soft"} or \code{"all"} is included, then it is replaced by all
hard and soft dependency.
\subsection{Extra dependencies}{

pak supports extra dependency types for direct
installations not from CRAN-like repositories.
These are specified with a \verb{Config/Needs/} prefix in the \code{DESCRIPTION}
and they can contain package references, separated by commas.
For example you can specify packages that are only needed for the
pkgdown website of the package:

\if{html}{\out{<div class="sourceCode">}}\preformatted{Config/Needs/website: r-lib/pkgdown
}\if{html}{\out{</div>}}

To use these dependency types, you need to specify them in the
\code{dependencies} argument to
pak functions.

Note that \verb{Config/Needs/*} fields are currently \emph{not} used from CRAN
packages, and packages in CRAN-like repositories in general.

Usually you specify that a \verb{Config/Needs/*} dependency type should be
installed together with \code{"hard"} or \code{"all"}, to install all hard or
soft dependencies as well.
}