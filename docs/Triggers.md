# Triggers: eventos que inician workflows en GitHub Actions

 - `push`: Se activa cuando se realiza un push a un repositorio, ya sea en una rama específica o en todas las ramas.

    ```yaml
    on: 
        push: 
            branches:
                - 'main'
                - 'releases/**'
            paths: 
                - '**.js'
    ```
                
 - `pull_request`: Se activa cuando se abre, actualiza o cierra un pull request en el repositorio.

    ```yaml
    on: 
        pull_request: 
            types:
            - [opened, labeled]
            branches:
                - 'releases/**'
            paths: 
                - '**.js'
    ```

 - `issues`: Se activa cuando se crea, cierra o etiqueta un issue en el repositorio.

    ```yaml
    on: 
        issues: 
            types: [opened, edited, closed]

    ```

 - `issue_comment`: Se activa cuando se agrega, actualiza o elimina un comentario en un issue.

    ```yaml
    on: 
        issue_comment: 
            types: [created, deleted]
    
    on: issue_comment
    jobs: 
        pr_commented:
            name: PR comment
            if: ${{ github.event.issue.pull_request }}
    ```

 - `workflow_dispatch`: Permite ejecutar un workflow manualmente desde la interfaz de GitHub.
    
    ```yaml
    on: 
        workflow_dispatch:
            inputs: 
                alert:
                    description: 'nivel'
                    required: true
                    default: medio 
                    type: choice 
                    options: 
                    - bajo 
                    - medio

    on: 
        workflow_dispatch:
            inputs: 
                tags:
                    description: 'Opcional'
                    required: true
                    type: booleand 
                environment: 
                    description: 'Objetivo'
                    type: string 
                    required: true
    ```

 - `schedule`: Se activa en un horario específico definido mediante cron (por ejemplo, diariamente o semanalmente).

    ```yaml
    on: 
        schedule:  
            - cron: '30 5,17 * * *'
    ```   

## Documentación
 - [Events Triggers]('https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#about-events-that-trigger-workflows')