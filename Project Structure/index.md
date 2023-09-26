# Project Structure

Akis Project is designed to work as an orchestration of different docker components.

!!!
Because of the nature of the project, the components are not independent. Updating one component may require updating the other components too.
!!!

These docker components are:

1. [Docker Compose](/project-structure/docker-compose/) - :brain: Main component that orchestrates the other components. :point_left:
2. [Services](/project-structure/services/)
3. [Volumes](/project-structure/volumes/)
4. [Networks](/project-structure/networks/)
