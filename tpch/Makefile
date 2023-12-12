SHELL=/bin/bash
PYTHON=.venv/bin/python

.venv:
	@python3 -m venv .venv
	@.venv/bin/pip install -U pip
	@.venv/bin/pip install --no-cache-dir -r requirements.txt

clean-tpch-dbgen:
	$(MAKE) -C tpch-dbgen clean

clean-venv:
	rm -r .venv

clean-tables:
	rm -r tables_scale_*

clean: clean-tpch-dbgen clean-venv

tables_scale_1: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 1 && cd ..
	mkdir -p "tables_scale_1"
	mv tpch-dbgen/*.tbl tables_scale_1/
	.venv/bin/python prepare_files_duckdb.py 1

tables_scale_5: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 5 && cd ..
	mkdir -p "tables_scale_5"
	mv tpch-dbgen/*.tbl tables_scale_5/
	.venv/bin/python prepare_files_duckdb.py 5 


tables_scale_10: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 10 && cd ..
	mkdir -p "tables_scale_10"
	mv tpch-dbgen/*.tbl tables_scale_10/
	.venv/bin/python prepare_files_duckdb.py 10

tables_scale_15: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 15 && cd ..
	mkdir -p "tables_scale_15"
	mv tpch-dbgen/*.tbl tables_scale_15/
	.venv/bin/python prepare_files_duckdb.py 15 

tables_scale_20: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 20 && cd ..
	mkdir -p "tables_scale_20"
	mv tpch-dbgen/*.tbl tables_scale_20/
	.venv/bin/python prepare_files_duckdb.py 20

tables_scale_50: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 50 && cd ..
	mkdir -p "tables_scale_50"
	mv tpch-dbgen/*.tbl tables_scale_50/
	.venv/bin/python prepare_files_duckdb.py 50 

tables_scale_100: .venv
	$(MAKE) -C tpch-dbgen all
	cd tpch-dbgen && ./dbgen -vf -s 100 && cd ..
	mkdir -p "tables_scale_100"
	mv tpch-dbgen/*.tbl tables_scale_100/
	.venv/bin/python prepare_files_duckdb.py 100 


run_polars: .venv
	.venv/bin/python -m polars_queries.executor

run_pandas: .venv
	.venv/bin/python -m pandas_queries.executor

run_dask: .venv
	.venv/bin/python -m dask_queries.executor

run_modin: .venv
	.venv/bin/python -m modin_queries.executor

run_vaex: .venv
	.venv/bin/python -m vaex_queries.executor

run_spark: .venv
	.venv/bin/python -m spark_queries.executor

run_duckdb: .venv
	.venv/bin/python -m duckdb_queries.executor

plot_results: .venv
	.venv/bin/python -m scripts.plot_results

run_all: run_polars run_duckdb run_spark run_pandas

pre-commit:
	.venv/bin/python -m isort .
	.venv/bin/python -m black .
