# task-9-of-Angie-
--
-- PostgreSQL database dump
--

-- Dumped from database version 14.11
-- Dumped by pg_dump version 14.11

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

SET default_tablespace = '';

SET default_table_access_method = heap;

--
-- Name: department; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.department (
    dept_no character varying(20) NOT NULL,
    dept_name character varying(50)
);


ALTER TABLE public.department OWNER TO postgres;

--
-- Name: dept_empl; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.dept_empl (
    emp_no integer NOT NULL,
    dept_no character varying(20) NOT NULL,
    de_id integer NOT NULL
);


ALTER TABLE public.dept_empl OWNER TO postgres;

--
-- Name: dept_empl_de_id_seq; Type: SEQUENCE; Schema: public; Owner: postgres
--

ALTER TABLE public.dept_empl ALTER COLUMN de_id ADD GENERATED ALWAYS AS IDENTITY (
    SEQUENCE NAME public.dept_empl_de_id_seq
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1
);


--
-- Name: dept_manager; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.dept_manager (
    dept_no character varying(20) NOT NULL,
    emp_no integer NOT NULL,
    dm_id integer NOT NULL
);


ALTER TABLE public.dept_manager OWNER TO postgres;

--
-- Name: dept_manager_dm_id_seq; Type: SEQUENCE; Schema: public; Owner: postgres
--

ALTER TABLE public.dept_manager ALTER COLUMN dm_id ADD GENERATED ALWAYS AS IDENTITY (
    SEQUENCE NAME public.dept_manager_dm_id_seq
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1
);


--
-- Name: emp; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.emp (
    emp_no integer NOT NULL,
    emp_title character varying(20) NOT NULL,
    birth_date date,
    first_name character varying(50),
    last_name character varying(50),
    sex character varying(10),
    hired_date date
);


ALTER TABLE public.emp OWNER TO postgres;

--
-- Name: salary; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.salary (
    emp_no integer NOT NULL,
    salary integer
);


ALTER TABLE public.salary OWNER TO postgres;

--
-- Name: titles; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.titles (
    title_id character varying(20) NOT NULL,
    title_name character varying(50)
);


ALTER TABLE public.titles OWNER TO postgres;

--
-- Name: department department_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.department
    ADD CONSTRAINT department_pkey PRIMARY KEY (dept_no);


--
-- Name: dept_empl dept_empl_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_empl
    ADD CONSTRAINT dept_empl_pkey PRIMARY KEY (de_id);


--
-- Name: dept_manager dept_manager_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_manager
    ADD CONSTRAINT dept_manager_pkey PRIMARY KEY (dm_id);


--
-- Name: emp emp_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.emp
    ADD CONSTRAINT emp_pkey PRIMARY KEY (emp_no);


--
-- Name: salary pk_emp_no; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.salary
    ADD CONSTRAINT pk_emp_no PRIMARY KEY (emp_no);


--
-- Name: titles titles_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.titles
    ADD CONSTRAINT titles_pkey PRIMARY KEY (title_id);


--
-- Name: dept_manager fk_dept_no; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_manager
    ADD CONSTRAINT fk_dept_no FOREIGN KEY (dept_no) REFERENCES public.department(dept_no);


--
-- Name: dept_empl fk_dept_no; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_empl
    ADD CONSTRAINT fk_dept_no FOREIGN KEY (dept_no) REFERENCES public.department(dept_no);


--
-- Name: salary fk_emp; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.salary
    ADD CONSTRAINT fk_emp FOREIGN KEY (emp_no) REFERENCES public.emp(emp_no);


--
-- Name: dept_manager fk_emp_no; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_manager
    ADD CONSTRAINT fk_emp_no FOREIGN KEY (emp_no) REFERENCES public.emp(emp_no);


--
-- Name: dept_empl fk_emp_no; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.dept_empl
    ADD CONSTRAINT fk_emp_no FOREIGN KEY (emp_no) REFERENCES public.emp(emp_no);


--
-- Name: emp fk_titles; Type: FK CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.emp
    ADD CONSTRAINT fk_titles FOREIGN KEY (emp_title) REFERENCES public.titles(title_id);


--
-- PostgreSQL database dump complete
--
