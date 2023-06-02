# 📦 NuGet Performance Monitor

The NuGet Performance Monitor is an automated system for monitoring the performance of the NuGet package manager. It
continuously runs benchmarks for new releases of NuGet, and in case of performance regressions, it raises an alert by
opening a new Issue in this repository. Visit the [dashboard](https://G-Research.github.io/NuPerfMonitor/) to see the
performance metrics.

## 🎯 Motivation

In our company, we work with .NET solutions containing hundreds of projects, and we prioritize developer productivity.
Therefore, we are deeply interested in improving the performance of the .NET ecosystem.

One of the key factors affecting developer productivity is the time spent waiting for NuGet to restore packages. We also
want to benefit from runtime improvements shipped with every new release of .NET. However, migrating to a new runtime
depends on being able to use the corresponding version of a .NET SDK and NuGet.

It happened in the past that there were some changes in NuGet that performed very poorly on large solutions, preventing
us from jumping to a newly released .NET until the bug was fixed. To prevent such unpleasant surprises in the future, we
have created NuGet Performance Monitor.

## 🚀 How it works

- [Scripts](https://github.com/NuGet/NuGet.Client/tree/dev/scripts/perftests) from
  the [NuGet.Client](https://github.com/NuGet/NuGet.Client) repository with
  custom [test cases](https://github.com/G-Research/NuPerfMonitor/tree/master/scripts/perftests/testCases) are used for
  benchmarks.
- GitHub Actions and GitHub-hosted runners are used to run benchmarks on
  a [daily schedule](https://github.com/G-Research/NuPerfMonitor/blob/master/.github/workflows/benchmarks.yml).
- Python script is used to [process results](https://github.com/G-Research/NuPerfMonitor/blob/master/process_results.py)
  and append them to the [data.csv](https://github.com/G-Research/NuPerfMonitor/blob/master/data.csv) file for easy
  plotting of charts and further data analysis.
- Another python script is used
  to [generate alerts](https://github.com/G-Research/NuPerfMonitor/blob/master/generate_alert.py). In case of
  performance regression, a new Issue is opened.
- [Plotly.js](https://plotly.com/javascript/) is used
  to [generate charts](https://github.com/G-Research/NuPerfMonitor/blob/master/_site/index.html) with results.

NuGet Performance Monitor uses GitHub-hosted runners to run the benchmarks, which ensures independence from the
infrastructure that is running it. Each test job runs two tests, one for the baseline version and one for the current
version, allowing for relative performance measurement.

## 🤝 Contributing

Contributions are welcome! If you have any suggestions or ideas to be implemented, we encourage you to:

- [File an issue](https://github.com/G-Research/NuPerfMonitor/issues/new/choose)
- [Submit a pull request](https://github.com/G-Research/NuPerfMonitor/pulls)

## 📄 License

This project is licensed under the [Apache License, Version 2.0](LICENSE).

