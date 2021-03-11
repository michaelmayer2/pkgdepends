# install_package_plan metadata

    Code
      plan <- make_install_plan(paste0("local::", pkg), lib = libpath)
    Message <cliMessage>
      i No downloads are needed, 1 pkg is cached
      v Got foo 0.0.0.9000 (source)
    Code
      plan$metadata[[1]] <- c(Foo = "Bar", Foobar = "baz")
      plan$vignettes <- FALSE
      install_package_plan(plan, lib = libpath, num_workers = 1)
    Message <cliMessage>
      i Building foo 0.0.0.9000
      v Built foo 0.0.0.9000
      v Installed foo 0.0.0.9000 (local)
      v Summary:   1 new
